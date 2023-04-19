ASP.NET controllers are never instantiated, so we need to configure it with a mechanism where we can inject it’s components such as services implicitly. .NET core supports and encourages DI by default

- In your Api project, through extension methods. We will create separate classes to inject separate pieces of codes (particularly services) to make it more SRP compliant
   - Folder Structure: Api > Extensions > Injection
- Each service e.g. UserService will have its own extension class that extends IServiceCollection and implements injection as illustrated below:

<IMG  src="https://lh3.googleusercontent.com/Ory9jiEXQvqY2G-P_qaP7Oh1UJQCkP3U-LoT5JO33jeWPvkk9DEMmUc6xclVntJdxo9velNnyMHLmsJrHl-x-pk8jWu1tWAGbeCvtO4B7u9Hv8S-GjoDPOnmOOGWlQAthNpqwCpa" />

- Which then be consumed in the Startup.cs class:

<IMG  src="https://lh6.googleusercontent.com/QJK5XydXBVc48AklGOe_BbKfj2W7oL2Mfp-2-lkP68q5xsSBK0Q7fqtHYyM0aShypitu_x8HUpOZ9-wPTIh_fO1Xqa7HhfGtu9kbAb3q25mKLP6ltiZ3U9ozz20tiE35UBdbnUAw" />

- Make sure to pass IConfiguration because some injection requires configured values such as connection strings or api keys.