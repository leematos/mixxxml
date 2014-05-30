# SUPER PRE ALPHA
Mixxxml is still being defined and heavily refined. it may not work at the moment.

---
##Mixxxml Syntax

Mixxxml has a very simple syntax that is very intuitive for beginners and experts alike. Check out the features below:

###Tags

The core of Mixxxml are tags. They look like this:


    tag: value

These directly translate into MIXXX XML tags to be parsed
by the mixxx app. Tags can also be nested like such with **two** space indentation:

    parent:
      child: value

Here is an example of a vumeter.mixxxml file and below the XML it outputs:

####vumeter.mixxxml
    Template:
      VuMeter:
       MinimumSize: 100,20
       MaximumSize: 200,20
       PathVu: vumeter.svg
       Horizontal: true
       PeakHoldSize: 5
       PeakHoldTime: 600
       PeakFallTime: 100
       PeakFallStep: 1
       Connection
         ConfigKey: {{group}},VuMeter

####vumeter.xml
    <!DOCTYPE template>
    <Template>
      <VuMeter>
        <MinimumSize>100,20</MinimumSize>
        <MaximumSize>200,20</MaximumSize>
        <PathVu>vumeter.svg</PathVu>
        <Horizontal>true</Horizontal>
        <PeakHoldSize>5</PeakHoldSize>
        <PeakHoldTime>600</PeakHoldTime>
        <PeakFallTime>100</PeakFallTime>
        <PeakFallStep>1</PeakFallStep>
        <Connection>
          <ConfigKey><Variable name="group"/>,VuMeter</ConfigKey>
        </Connection>
      </VuMeter>
    </Template>

### Variables
In the above mixxxml code example, you may have noticed something interesting:

    {{group}}

This is a variable. This allows you to leverage the new variable features of mixxx 1.12
theming to make templating easier. To set a variable you can use the following syntax:

    Set(something): value

this will generate the following XML:

    <SetVariable name="something">value</SetVariable>

###Functions

In the last section we exposed you to your first function, ```Set()```. Functions have parens after their name.
Mixxxml functions wrap complex logic into a simple declarative syntax to keep your documents readable and clear.
Mixx functions are listed below:

#### Set(name): value
The set function has two modes, single assignment and multiple assignment. They look like this:

    Set(something): value

This is single assignment and it outputs the following:

    <SetVariable name="something">value</SetVariable>

The multi-assignment use looks like this:

    Set():
      item1: val1
      item2: val2
      item3: val3

The output looks like this:

    <SetVariable name="item1">val1</SetVariable>
    <SetVariable name="item2">val2</SetVariable>
    <SetVariable name="item3">val3</SetVariable>

This is useful when you need to set a lot variables for something like template overloading which is shown in the ```load()``` example below.

####Load(template_name):

The load function allows you to load sub templates into your skin.

    load(template.xml):

will make the following xml:

    <Template src="skin:template.xml"/>

If you wanted to pass variables into this template you could do the following:

    load(template.xml):
      Set():
        item1: val1
        item2: val2
        item3: val3

This generates:

    <Template src="skin:template.xml">
      <SetVariable name="item1">val1</SetVariable>
      <SetVariable name="item2">val2</SetVariable>
      <SetVariable name="item3">val3</SetVariable>
    </Template>

---
#Todo

1. Build a whole theme with mixxxml to find edge cases.
1. Define other necessary functions. (ConfigKey, Widget w/ triggers, others?)
1. fix XML generator.
