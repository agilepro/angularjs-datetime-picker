Simple DateTime Picker For AngularJS
===================================

No JQuery, No Bootstrap, Just AngularJS (ver. 1.3+)

#Origin

This is a pretty awesome date-time picker developed by [Gillardo](https://github.com/Gillardo/bootstrap-ui-datetime-picker) who deserves al the credit.  It is light.  It is compact on the screen.  And it allws the user to easily set both date and time conveniently without a lot of extra clicking through a lot of screens.

But it wasn't working for me because Date() objects don't function in JSON, and string formatted dates have lots of problems not the least of which is timezone related.  Here is what I need:

* Something that allows the user to set both date and time in a single control.  date/time pickers that represent date and time as separate spots onthe form does not work because then you have two controls and users have to manipulate those separately adding clicks.
* Supports standard Angular bi-directional behavior: anyone can set the value from anywere, and it updates everywhere.
* Display and edit in the users timezone even though the value is in universal time.
* True MVC such that the object member I get from the server is exactly the object member we edit.  JSON can not handle Date objects.  Transferring dates as long 'epoch' values is both universal and uncomplicated.  See all the reasons [here](https://agiletribe.wordpress.com/2015/06/10/jsonrest-api-handling-dates/).
* The picker must read the date as an integer, and write it back as an integer.  No need to copy the value out of an object, put it tranformed into another variable, edit that, and then put it back.

I have used many date pickers.  If they cover date without time it is useless for things like scheduling appointments because in different time zones, the date changes at different times.   Editing date by itself, and time by itself, leaves you with a complicated form.  Most of the time peole worry about the date, so we want that to be easy and not have to worry about the time, But occasionally you need the time and then it should be right there.   The original datetime picker did all this well.

There are a few datetime, but they all generally expect the input and output to be date objects.  That is fine if you are using client-only data structures, but if you are doing everything on JSON REST calls, the objects you get from the server can not have Date objects in them.   To make this work, you have to convert values after the object is received, and convert values before sending it out.  This also means you have two copies of all the date values, which is a debugging and development issue -- it is easy to make a mistake and update the wrong one, or update the right one at the wrong time.

This date-time picker seems to be in maintenance mode with no active changes nor active bug fixing.  Because of this, I felt it was expedient to simply fork the repository, and then change the way it works to read dates as epoch values, and writing back as epoch values. I don't ever anticipate needing any other format for communicating dates.  The original picker had some code to detect the type, and do the right thing, but this becomes convoluted, and it is tricky because if any of the JS code writes the wrong value in there, then that error get propogated.  Instead, I wants something that would detect and warn about this kind of problem quickly, so that coding errors are discovered quickly.

So that is what is it, the original EXCELLENT working data-time picker, but modified to work directly on long epoch value, reading and writing those values directly to the JSON bojects that go to and from the server.

Below is the messaging from the original project.





# Original ReadME

[DEMO](https://rawgit.com/kineticsocial/angularjs-datetime-picker/master/index.html)
[![Imgur](http://i.imgur.com/UJfYMN6.png?1)](https://rawgit.com/kineticsocial/angularjs-datetime-picker/master/index.html)

To Get Started
--------------

For Bower users,

  `$ bower install angularjs-datetime-picker`

1. Include `angularjs-datetime-picker.js` and `angularjs-datetime-picker.css`

        <link rel="stylesheet" href="angularjs-datetime-picker.css" />
        <script src="angularjs-datetime-picker.js"></script>

2. add it as a dependency

        var myApp = angular.module('myApp', ['angularjs-datetime-picker']);

3. Use it

        <input datetime-picker ng-model="model" />

Attributes
------------

  -  date-format: optional, date format e.g. 'yyyy-MM-dd'
  -  year: optional, year selected, e.g. 2015
  -  month: optional, month selected, e.g. 5
  -  day: optiona, day selected, e.g. 31
  -  hour: optional, hour selected, 23
  -  minute: optional, minute selected, 59
  -  date-only: optional, if set, timepicker will be hidden
  -  future-only: optional, if set, forces validation errors on dates earlier than now

Examples
--------

    <input ng-model="date1" datetime-picker date-only />

    <input ng-model="date1" datetime-picker date-only future-only />

    <input ng-model="date2" datetime-picker date-format="yyyy-MM-dd" date-only />

    <input ng-model="date3" datetime-picker date-format="yyyy-MM-dd HH:mm:ss" />

    <input ng-model="date4" datetime-picker hour="23" minute='59'/>

    <input ng-model="date5" datetime-picker date-format="yyyy-MM-dd HH:mm:ss" year="2014" month="12" day="31" />

