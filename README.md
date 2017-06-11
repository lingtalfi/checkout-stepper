Checkout Stepper
====================
2017-06-11


A checkout stepper helper for e-commerce.





How to?
==========

**checkout-stepper.js** is in this repository.


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="/theme/lee/libs/jquery/jquery-3.2.1.min.js"></script>
    <script src="/theme/lee/libs/checkout-stepper/checkout-stepper.js"></script>

    <style>
        .checkout-stepper > div {
            border: 1px solid #ddd;
            box-sizing: border-box;
            padding: 10px;
            margin: 10px;
            display: none;
        }

        .checkout-stepper > div.step-open {
            background: rgba(0, 255, 0, 0.3);

        }

    </style>
</head>

<body>

<div class="checkout-stepper">
    <div class="step-1 step-notset">
        Step 1: Your address (not set)
    </div>
    <div class="step-1 step-open">
        Please enter your address (open)
    </div>
    <div class="step-1 step-done">
        Your address: 6 wall street (done)
    </div>
    <div class="step-2 step-notset">
        Step 2: Your payment (not set)
    </div>
    <div class="step-2 step-open">
        Please choose your payment method (open)
    </div>
    <div class="step-2 step-done">
        Your payment method: credit card XXXXX-96 (done)
    </div>
    <div class="step-3 step-notset">
        Step 3: Your carrier (not set)
    </div>
    <div class="step-3 step-open">
        Please review the carrier details (open)
    </div>
    <div class="step-3 step-done">
        Your carrier: UPS-postIt (done)
    </div>
</div>


<div id="api-demo-buttons">
    <button class="markdone" data-id="1">Mark step 1 as done</button>
    <button class="open" data-id="1">Open step 1</button>
    <button class="open" data-id="2">Open step 2</button>
    <button class="open" data-id="3">Open step 3</button>
</div>


<script>
    $(document).ready(function () {

        var stepper = new CheckoutStepper({
            start: 1,
            context: $('.checkout-stepper')
        });


        $('#api-demo-buttons').on('click', function (e) {
            var jTarget = $(e.target);
            var stepNumber = jTarget.attr("data-id");
            if (jTarget.hasClass("open")) {
                stepper.openStep(stepNumber);
                stepper.markStepAsDone(stepNumber);
            }
            else if (jTarget.hasClass("markdone")) {
                stepper.markStepAsDone(stepNumber);
            }
            return false;
        });

    });
</script>
</body>
</html>





```



How does it work?
===================

We want to create a checkout form.
A checkout form is composed of multiple steps.

For instance:
 
- step 1: choose the shipping address
- step 2: choose the payment method
- step 3: choose the carrier method


You can have more/less steps, the steps don't need to be related to e-commerce.

Each step has three possible states, although only one step can be displayed at the time.

The three possible states are:

- notset
- open
- done


Typically, a step starts with the notset state.
Then you open it, and it switches to the open state.
From when the user successfully complete the step, it's marked as done (i.e. done state).
 
 
To create a step, you need to create a html element (like a div for instance) with class step-$n,
where $n is the number of the step, starting at 1, and being continuously +1 incremented (i.e. 
you can't create discontinuous steps otherwise it won't work),
and also class step-$state, where $state is one of the possible states.

This mean you need to create 3 html elements per step (one for each state).

Once you've done your markup right (see the above example for a quickstart), 
the CheckoutStepper object is ready to help you.

You just call the openStep method whenever you wish to open a step.

This method will open the step you want, and put all the other steps in either the done state, or the notset state,
depending on whether or not the step previously reached the done step.

For instance if you have 3 steps and you open step 2, 
then step 2 is open,

step 1 is switched to done if it was in the done state, or it switches to notset otherwise.
Same for step 3.

To mark a step as done, use the markStepAsDone method.








History Log
------------------    
    
- 1.0.0 -- 2017-06-11

    - initial commit
