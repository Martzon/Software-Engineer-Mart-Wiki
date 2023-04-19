`FormService` class
```
import * as functions from 'firebase-functions';
import Hubspot from 'hubspot';

/**
 * Wraps the calls to HubSpot Forms API
 */
export class FormService {
  constructor(
    private client: Hubspot,
    private logger = functions.logger
  ) {
    if (!client) {
      throw new Error('HubSpotClient is required');
    }
  }

  async getForms(): Promise<Record<string, any>[]> {
    try {
      const result = await this.client.forms.getAll();
      await Promise.all(result.map(async (form: any) => {
        try {
          form.lastSubmission = (await this.client.forms.getSubmissions(form.guid)).results[0];
        } catch (e) {
          // If no lastSubmission data, that is OK
        }
      }));
      return result;
    } catch (e) {
      // Log with service name and function
      this.logger.error('FormService::getForms', e);
      throw e;
    }
  }
}
```


`FormService` `Test` class
```

// Test Framework Setup
import 'mocha';
import 'chai-as-promised';
import { default as sinon } from 'ts-sinon';
import * as chai from 'chai';
import * as sinonChai from 'sinon-chai';
const expect = chai.expect;
chai.use(sinonChai);
chai.use(require('chai-as-promised'));

// Class to be Tested Setup
import { FormService } from './../../src/services/form.service';

describe('FormService', () => {
  // Declare all dependencies to be stubbed
  let clientStub: any;
  let loggerStub: any;
  let service: FormService;

  beforeEach(() => {
    // Stub out all methods used by using `sinon.stub()`
    // use `sinon.spy()` to assert `isCalled` using `.to.have.been.called...`
    clientStub = sinon.stub();
    clientStub.forms = sinon.stub();
    clientStub.forms.getAll = sinon.stub();
    clientStub.forms.getSubmissions = sinon.stub();
    loggerStub = sinon.stub();
    loggerStub.error = sinon.spy();

    service = new FormService(clientStub, loggerStub);
  });

  describe('getForms', () => {
    describe('Unsuccessful API call', () => {
      const error = new Error('Unsuccessful call');
      beforeEach(() => {
        clientStub.forms.getAll.throws(error);
      });

      it('should log the error with correct parameters', async () => {
        // Wrap this in try-catch so that chai won't expect a "throw"
        try {
          await service.getForms();
        } catch (e) {
          expect(loggerStub.error).to.have.been.calledWith('FormService::getForms', error);
        }
      });
    });

    describe('Successful API call', () => {
      const stubForms = [{ id: 1, }, { id: 2 }];
      const stubSubmission = { results: [{ id: 1 }] };

      beforeEach(() => {
        clientStub.forms.getAll.returns(Promise.resolve(stubForms));
        clientStub.forms.getSubmissions.returns(Promise.resolve(stubSubmission));
      });

      it('should respond with expected forms data', async () => {
        const result = await service.getForms();
        expect(result).to.equal(stubForms);
      });

      it('should respond with expected forms data even when there were no last submissions', async () => {
        clientStub.forms.getSubmissions.returns(Promise.reject(null));
        const result = await service.getForms();
        expect(result).to.equal(stubForms);
      });
    });
  });
});
```