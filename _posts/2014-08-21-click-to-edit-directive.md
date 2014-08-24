---
layout: post
title: AngularJS Directives
summary: Using AngularJS Directive to create a 'click to edit' field based on Jira user interfaces. Also, a little fun experimenting with jsfiddle embed.
---

So I was evaluating Crucible for code reviews a few days ago and was struck by the overall 'user friendliness' of the Atlassian suite of tools. One simple aspect I loved was the 'click to edit' fields. So I set out to use an AnguarJS directive (mixed with bootstrap and some simple css) to recreate this behavior. My fields are not as slick as Atlassian's but it's a good starting point. The full example below, followed by a ```step by step``` walkthrough of the features.

<iframe width="100%" height="395" src="http://jsfiddle.net/joshwood/hdvz7hpf/7/embedded/result,html,css,js,resources" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

###Step 1 : Create State 1 - hover mode
The first goal is to achieve the mouse-over or hover behavior. We'll create a border with rounded corners and an ```edit pencil``` to the right of the text field. We're using bootstrap glyphs to create the ```edit pencil```. The ```edit pencil``` div is hidden until :hover. The rendering and code is below (jsfiddle embed is just great).

<iframe width="100%" height="300" src="http://jsfiddle.net/joshwood/hdvz7hpf/embedded/html,css,resources,result" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

###Step 2 : Create State 2 - edit mode
Now we need to create ```state 2``` which is the field in ```edit mode```. In this state we will see a text input, a checkbox icon and a close icon to indicate 'save' or 'cancel' respectively. We're using bootstrap glyphs again for this.

<iframe width="100%" height="300" src="http://jsfiddle.net/joshwood/hdvz7hpf/1/embedded/html,css,resources,result" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

###Step 3 : Toggle between states
Now that we have created the 2 states of the field, we need to add click events to toggle from one state to the other. This is where the angular directive introduced. Because I'm using JSFiddle to help with this post I will embed the template sketch we just created in the JavaScript itself. The template can also be externalized into its own html file. Below we have the start of our directive that includes a ```toggle()``` function to switch between modes. As you can see the markup becomes very simple as the template code is included via the ```click-to-edit``` attribute.

<iframe width="100%" height="300" src="http://jsfiddle.net/joshwood/hdvz7hpf/2/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

###Step 4 : Data binding with save/cancel events
Next we'll need to actually use data from the model and introduce ```save``` and ```cancel``` functionality. To this point we have not defined a controller but now it will be required to setup bindings to model elements. We will pass the model element ```sprintName``` (from our new controller WidgetsController) into our directive as ```ng-model```. We also need to clone the model element so we can rollback edits when the user clicks cancel. To see this in action, make an edit and click cancel - you should see the original value restored. And obviously if you hit save it will update the model element. One thing to notice is the use of ```$timeout```. This allows dom rendering to happen before trying to set focus or blur. [found on stack](http://stackoverflow.com/questions/14833326/how-to-set-focus-on-input-field-in-angularjs)

<iframe width="100%" height="300" src="http://jsfiddle.net/joshwood/hdvz7hpf/3/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

###Step 5 : More [Plagiarism](http://stackoverflow.com/questions/17470790/how-to-use-a-keypress-event-in-angularjs) - enter key to save
The last bit of improvement will be to allow the user to simply hit the enter key to commit the changes. For that, I am adding another directive called ng-enter. It captures the ```keydown``` and ```keypress``` events looking for the enter key. It will call its function param upon hearing the enter key ```ng-enter="save()"```. I completely ripped off this directive and have notated it in the source. It is a wonderful demonstration of how directives should be used.

<iframe width="100%" height="350" src="http://jsfiddle.net/joshwood/hdvz7hpf/6/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>
























