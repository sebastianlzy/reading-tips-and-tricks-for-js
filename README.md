# reading-tips-and-tricks-for-js
A collection of tips and tricks for JS development

### Patterns
#### Module Pattern

[https://addyosmani.com/largescalejavascript/](https://addyosmani.com/largescalejavascript/)

The module pattern is a popular design that pattern that encapsulates 'privacy', state and organization using closures. It provides a way of wrapping a mix of public and private methods and variables, protecting pieces from leaking into the global scope and accidentally colliding with another developer's interface. With this pattern, only a public API is returned, keeping everything else within the closure private.

```
var basketModule = (function() {
    var basket = []; //private
    return { //exposed to public
        addItem: function(values) {
            basket.push(values);
        },
        getItemCount: function() {
            return basket.length;
        },
        getTotal: function(){
           var q = this.getItemCount(),p=0;
            while(q--){
                p+= basket[q].price; 
            }
            return p;
        }
    }
}());
```

#### The Facade Pattern

[https://addyosmani.com/largescalejavascript/](https://addyosmani.com/largescalejavascript/)

The reason the facade is of interest is because of its ability to hide implementation-specific details about a body of functionality contained in individual modules. The implementation of a module can change without the clients really even knowing about it.

```
var module = (function() {
    var _private = {
        i:5,
        get : function() {
            console.log('current value:' + this.i);
        },
        set : function( val ) {
            this.i = val;
        },
        run : function() {
            console.log('running');
        },
        jump: function(){
            console.log('jumping');
        }
    };
    return {
        facade : function( args ) {
            _private.set(args.val);
            _private.get();
            if ( args.run ) {
                _private.run();
            }
        }
    }
}());

```

The core difference between the facade pattern and the mediator is that the facade (a structural pattern) only exposes existing functionality whilst the mediator (a behavioral pattern) can add functionality.

#### The Mediator Pattern

[https://addyosmani.com/largescalejavascript/](https://addyosmani.com/largescalejavascript/)

Mediators are used when the communication between modules may be complex, but is still well defined. If it appears a system may have too many relationships between modules in your code, it may be time to have a central point of control, which is where the pattern fits in.

Consider modules as publishers and the mediator as both a publisher and subscriber. Module 1 broadcasts an event notifying the mediator something needs to done. The mediator captures this message and 'starts' the modules needed to complete this task Module 2 performs the task that Module 1 requires and broadcasts a completion event back to the mediator. In the mean time, Module 3 has also been started by the mediator and is logging results of any notifications passed back from the mediator.

Notice how at no point do any of the modules directly communicate with one another. If Module 3 in the chain were to simply fail or stop functioning, the mediator could hypothetically 'pause' the tasks on the other modules, stop and restart Module 3 and then continue working with little to no impact on the system. This level of decoupling is one of the main strengths the pattern has to offer.

### References
1. [Currency Formatting using REGEX](https://blog.tompawlak.org/number-currency-formatting-javascript)
