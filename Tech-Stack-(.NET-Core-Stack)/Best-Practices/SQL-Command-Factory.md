A class that is responsible for creating commands that the data gateway uses. This also promotes Single Responsibility Principle by taking away the creation of SqlCommands away from the data gateways. These classes should:
- Only return `SqlCommand`
- Be responsible on setting which query or stored procedure to use and
- Adding/building parameters for the command
