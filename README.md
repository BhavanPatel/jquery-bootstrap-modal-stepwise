# jquery-bootstrap-modal-steps
Lightweight step by stepwise modal for bootstrap

## What is this?
Sometimes you need break complex things in many parts. Forms, manuals, ideas. I like to thing that like steps. 
For example, if you need create a payment page. The first step is get the personal information from the client, 
then you need the payment information and after that you'll need the address for the shipment. 
This is not the correct order but works.

You can develop a big HTML form with all this stuff or ask to client in step by step.

## What I need?
You'll need to know about bootstrap, html and a little bit of javascript.
jQuery and Bootstrap must be installed in your project.

## How to install

Using Bower:  
`$ bower install jquery-bootstrap-modal-stepwise`


## How to uninstall

Using Bower:  
`$ bower uninstall jquery-bootstrap-modal-stepwise`

jQuery and Bootstrap are required so you need import them in your Html file before jquery-bootstrap-modal-steps:

```html
<script src="http://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.1/jquery.min.js"></script>
<script src="http://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.2.0/js/bootstrap.min.js"></script>

<script src="../dist/modal-steps.min.js"></script>
```

## Configuring the Modal

Is pretty simple to work with Bootstrap modals. You can see more details [here](http://getbootstrap.com/javascript/#modals).
 ```html
<div class="modal-header">
    <h4 class="js-title-step"></h4>
</div>
```

In your `.modal-header` you'll need use any Html tag with **js-title-step** class. I decide for H4 for estetic purposes.
**Don't put nothing inside this tag**, the Javascript will do this.

After that, at the `.modal-body` you'll set the modal steps. Use a `div` tag with **row** and **hide** class.
Set the step order using **data-step** and step title with **data-title**.
```html
<div class="modal-body">
    <div class="row hide" data-step="1" data-title="This is the first step!">
        <div class="jumbotron">As you can see, this is the first step!</div>
    </div>
    <div class="row hide" data-step="2" data-title="This is the second and last step!">
        <div class="jumbotron">As you can see, this is the second and last step!</div>
    </div>
</div>
```

Now, you'll set the action buttons. All you need is use **js-btn-step** and **data-orientation** attribute.
Use `data-orientation="previous"` for previous buttons, `data-orientation="next"` for next buttons, and 
`data-orientation="cancel"` for cancel buttons.

```html
<div class="modal-footer">
    <button type="button" class="btn btn-default js-btn-step pull-left" data-orientation="cancel" data-dismiss="modal"></button>
    <button type="button" class="btn btn-warning js-btn-step" data-orientation="previous"></button>
    <button type="button" class="btn btn-success js-btn-step" data-orientation="next"></button>
</div>
```
Note you don't need set nothing inside the **.js-btn-step**.

## Activate modals

You already have the modal, now you'll need activate it.

```javascript
$('#modal-sample').modalSteps();
```

With this you can use steps with Bootstrap modals.

**Don't forget that you need use a button to launch the Bootstrap modal**.
You can see more of this [here](http://getbootstrap.com/javascript/#modals-usage)

## It's jQuery
You can use jQuery functions after modalSteps because this is a jQuery plugin (haha):
```javascript
$('#modal-sample').modalSteps().find('#someDiv');
```

## Callbacks
### Using a callback when user complete modal's steps
You can set a callback when the user completes the modal steps.

```javascript
var callback = function (){
    console.log('Congratulations!');
};

$('#modal-sample').modalSteps({
    completeCallback: callback
});
```

### Callback for each step
When you need valid forms in each modal step, it's cool a callback for this
```javascript
var callback = function (){
    console.log('Each step Callback!');
};

$('#modal-sample').modalSteps({
    callbacks: {
        '*': callback
    }
});
```

### Callback for a specific step
Generally, you'll have a step pretty different of others and you must treat that.
Use an specific callback for this. The key of the callback dictionary must be the step:
```javascript
var callback1 = function (){
    console.log('A specific callback for step 1!');
};

var callback2 = function (){
    console.log('A specific callback for step 2!');
};

$('#modal-sample').modalSteps({
    callbacks: {
        '1': callback1,
        '2': callback2
    }
});
```


### Get Title and Current Step for each step
When you need title and current step from in each modal step, it's cool do this
```javascript
var callback = function (title,step){
    console.log('Each step Title!',title);
    console.log('Each step Step!',step);
};

$('#modal-sample').modalSteps({
    getTitleAndStep: function(title, step) {
        callback(title, step);
    }
});
```


## Customize buttons
The default values for buttons is:

Button Orientation | Value
------------------ | -------
previous|Previous
next|Next
cancel|Cancel
last|Complete

### How to replace?
```javascript
$('#modal-sample').modalSteps({
    btnCancelHtml: 'Quit',
    btnPreviousHtml: 'Back',
    btnNextHtml: 'Go',
    btnLastStepHtml: 'Finish'
});
```

### Disabling next buttons
For validations purposes, you can need block the next buttons:
```javascript
$('#modal-sample').modalSteps({
    disableNextButton: true
});
```
