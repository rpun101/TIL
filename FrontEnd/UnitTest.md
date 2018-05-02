
## Unit Testing in Angular ##

[codecraft.tv](https://codecraft.tv/courses/angular/unit-testing/overview/)  
**Unit Testing**: isolated tests  
**Functional Testing**: e2e, as if application was rendered in browser and user is interacting with the page.

### Write and Run Tests using Jasmine & Karma. ###
1. Jasmine
    + Behavior-Driven Development(BDD)
    + 
    ```js
    describe("A test suite is just a function", function(){
        var a;

        /* setup and teardowns for each it(test spec)
        [beforeEach(function), beforeAll(function), afterEach(function), afterAll(function)]  
        */
        it("and so is a test spec", function(){
            a = true;
            expect(a).toBe(true); /* expected(actual).matcher(expectedValue) */
        });
    });
    ```
    + Pre-pending with letter `x` disables test suite or spec, while letter `f` focus on test
    ```js
    // disable this test suite
    xdescribe(string, function(){
        xit(string, function);
    });
    //run this test onlyh
    fdescribe(string, fucntion);
    ```
1. Karma
    + _Problem_: manually testing jasmine for each browser is tiresome and unproductive
    + lets us spawn browses and run jasmine tests
    + watches development files for changes and re-runs tests

### Testing Classes ###
> Everything in Angular is an instance of a class, be it a `Component`, `Directive`, `Pipe`   

+ pipes are simplest form in Angular class. We can test pipes, if it doesn't have dependencies, like a class.  

+ 
    ```ts
    //auth.service.ts
    export class AuthService {
        isAuthenticated(): boolean {
            return !!localStorage.getItem('token');
        }
    }
    //auth.service.spec.ts
    import {AuthService } from './auth.service';

    describe('Service: Auth', ()=>{
        let service: AuthService();
    });

    beforeEach(()=> {
        service = new AuthService();
    });

    afterEach(()=> {
        service = null;
        localStroage.removeItem('token');
    });

    it('should return true from isauthenticated when there is token', ()=>{
        localStorage.setItem('token', '1234');    //this is spec only data
        expect(service.isAuthenticated()).toBeTruthy();
    })

    ```

### Testing with Mocks & Spies ###  

**Mocking** is act of creating something that looks like the dependency but is something we control in out test.   

1. Mocking with fake classes  
    **_problem_** Creating a new class inside a class creates a tight coupling. To test one class, one has to create all the dependent classes. This is not good, it is anti pattern and hard to code to, hard to debug and it increases the complexity.  
    **_solution_**: Most modern programming use dependency injection to loosely couple classes. To test this class other class functionality is mocked. which means to test a class in isolation  

    > Mocking is act of creating something that looks like the dependency but is something we control in our test.   

    Instead of creating fake class, we can `extend` the class then the override the function we need.    
    ```js
    class MockAuthservice extends AuthService {
        authenticated = false;
        isAuthenticated() {
            return this.authenticated;
        }
    }
    ```
1. Mocking by using a real instance with Spy  
> Spy is feature of Jasmine which lets you take an existing class, function, object and _mock_ it in such a way that you can control what gets returned from functions.  

    ```js
    spy = spyOn(service, 'isAuthenticated').and.returnValue(false);
    ```  

### Angular Test Bed (ATB) ###

+ higher level _Angular Only_ testing framework which makes easier to create components, handle injection, test asynchronous behavior and interact with our application.  
