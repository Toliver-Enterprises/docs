---
title: "Wizard"
id: ""
---

**UI** are suitable for tasks that have **independent steps,** wherein the user is taken through each step to comprehend the task in a structured manner. Wizards have steps with a specific UI style that facilitates easy navigation. Wizards provide **and next step buttons** for the user to confirm their selections/actions in each of these steps. Users can also the task at any step. Wizards also provide Done or Finish button at the end of the final step, to indicate that all the steps are finished.

can be many **case scenarios** where a wizard can be used. Examples of some common use cases are as follows:

1. \-line Payments
2. Orders
3. of Documents
4. Installations
5. Accounts in Websites
6. /App Configurations

[![](../assets/WZ_concept.png)](../assets/WZ_concept.png)

**widget** facilitates the user through the procedural interface to perform tasks in a specific pre-defined order.

1. Wizard widget has **step by default** and user can add multiple steps using the Wizard **Step** property.
2. **Step button** is added to all steps except the last step where a **button** is used to complete the wizard process.
3. **Step button** is added to all steps except the first step.
4. Caption for Action Buttons: [![](../assets/WZ_props.png)](../assets/WZ_props.png)

- **and Previous**: To navigate through the steps of the wizard we have Next and Previous buttons in the wizard widget. The caption for these buttons can be changed using the Next caption and Previous caption properties available in the Wizard basic properties. The captions are also bindable.
- **and Cancel Buttons**: The Wizard also has a Done and Cancel Button which perform actions for Completion of the task or for Canceling of the task respectively. These button captions can be changed using the Cancel action caption and Done action caption properties respectively. Each of the above captions is also bindable.
- **and Done Buttons**: These buttons can be disabled from the Script using the and properties. For example, using \= !paymentOption.datavalue;, will enable the Done button only when a payment option is checked.
- - **Style:** can be set as auto or justified
    - **Step**: bindable property acting as the starting point for the wizard. For instance, if default step is set to step 3, then at runtime the third step is the active step on a load of the wizard with the previous two steps marked as complete. [![](../assets/WZ_defaultstep.png)](../assets/WZ_defaultstep.png)
- : property of the wizard can be used to show/hide the wizard based on a variable’s value. Show feature is bindable and can be bound to a boolean field in a dataset.
- in Wizards: [![](../assets/WZ_events.png)](../assets/WZ_events.png) The callback events for Wizard will fire on the trigger of the specific event:
- **:** This is a callback which fires when the Done button is pressed at the end. For Example, when Done button is clicked by the user, the order status can be set to Order Shipped and Tracking Details page can show up.
- **:** This is a callback which fires when the Cancel button is pressed at the end of the steps.

### Step Features

**UI** is designed with a unique style to differentiate from a tab and to start with the first step will be enabled and the remaining steps are disabled. Each of these steps has the following features that can be manipulated.

1. : This is the title that appears on the step, which is changed by the user in the wizard step properties. [![](../assets/WZ_steptitle.png)](../assets/WZ_steptitle.png)
2. : The content can only be an inline content which means that you have to design each step of the wizard like you design every page in WaveMaker. You cannot use partial content in any step of the wizard.
3. : consists of the following properties that can be configured:

- **:** Wizard step can be shown or hidden by checking it on/off. The step can also be shown or hidden by binding the show property to a boolean field.
- **Skip**: This feature will allow you to skip a step and jump to next step. This can be turned on or off in the wizard step properties. It appears only as a link when turned on and at run-time when clicked it moves to the next step without doing anything in the current step.  The user can plugin JavaScript handlers to apply some logic when the skip link is clicked.
- Step Features include:
    - **Next**: This feature is not exposed as a property in the wizard and it is only available through scripting. The user can avail this feature by writing a JavaScript to disable the next step that can get invoked on Load event of the step to be disabled. Disable Next will be useful if the user has provided some information in the current step wherein next step information may become irrelevant to the user. For example: In an Employee Application form Wizard, there may be some step which would expect the user to provide information regarding previous employment. If the user has entered No for a question on Previous Employment in the current step and if the next step is for giving details on Previous Employment, Disable Next is a viable option.
    - **Done button**: This feature is also not exposed as a property in the wizard widget and it is only available through scripting. This can be done by on Load event of that step. The user can write a javascript function to enable Done button in a step if responses and actions for the step by the user are good enough to complete the task at that step itself. In the case of Configuration Management, a Config Wizard can take you through many steps wherein some initial steps will be mandatory and later steps may be for an advanced user. In that case, the Done button can be enabled in the step where all basic information has been provided by the user so that user can complete the task.
- **Step Events**: There are callback events for every wizard step that will fire on the happening of such events. Based on user entries and confirmations in the current step, the next step contents can be populated. Wizard scope and step scope will be passed as an argument to the respective callback event. Hence, your javascript function will have access to the Wizard scope and step scope.
    - **Load**: This is a callback which fires when onLoad of the particular step happens and only the wizard scope will be passed on to the callback event. If a user is writing a JavaScript function to handle this event, the user will be able to access the wizard scope and using that can access any widgets in that scope. OnLoad on a step can be used to populate some values in a widget based on other widgets. For example, one can populate the orders pending for a department based on the Dept id or Name.
    - **Next**: This is a callback which fires when the next step button is clicked by the user in a step. When the event fires the wizard scope and step scope will be passed as arguments to On Next callback. If you plan to invoke a JavaScript function when the event occurs, you will be able to have access to these scopes and access the widgets with respect to wizard scope and access the properties with respect to the steps. This can be used to do some updates to a field based on the user’s response in the step and the next step can show the result of the updates made. For example, once the user confirms the order, the order status field in the orders table can be set to Confirmed and it can take the user to payment step.
    - **Prev**: This is a callback which fires when the Previous button is clicked by the user in a step. When the event fires the wizard scope and step scope will be passed as arguments to On Prev callback. If you are implementing a JavaScript function to invoke when the event occurs, you will be able to have access to these scopes within your function. The user can make some edits or deletes to some content in the previous steps. For example, once the user has added items to the cart in one step and has moved to next step and later decides to remove that from the cart, the user can use the previous step to make such edits.
    - **Skip**: You will be able to skip steps by enabling skip on these steps by setting the Enable Skip property on the step to on. Once Enable Skip is on, the user will be able to see a Skip link at the left bottom of the wizard in the step for which Enable Skip is on. This callback fires when the skip link is clicked by the user in that step. If the user wants to set some defaults for the required fields in the step before he jumps to the next step, he can handle this callback. On Skip event will not take the scopes as arguments. The user can use this in case you want to assign some flags or some required values to some of the fields in the respective step UI. The user can also skip in case he does not have the necessary details to complete that step. While Registering an Account in any e-commerce site, after giving the profile information, the wizard may have one of the steps which asks for payment related details like credit card number etc. We normally skip that step as it is not necessary to provide that information while registering.

### in Wizard

- step in the wizard can have any kind of widgets depending on the usage scenario – for example -Live form widget, Data Table Widget, a list widget, Grid Layout with Label and Text Widgets.
- Widgets are to be dragged and dropped into Wizard Step Area. Once a step is selected, the wizard step is highlighted and the appropriate widget can be dropped on that area.
- user entries in a step, the recommended widget is a Live Form where the wizard’s next button of that step will be disabled until all required fields in a form are entered by the user. The validations which are by default available in a form will be available within the wizard step also.
- can also have a Dialog and drag and drop a wizard into the Dialog which will give a Dialog with steps which can be hidden once the steps are completed by clicking the Done button on the wizard.
- can drag and drop any Live and Data widgets as well as basic widgets onto a wizard step.

# Scenarios

basic usage scenario is used to go through the wizard interface step by step trying to build a Registration Form. A **Registration Form** that can be used by any websites to get their users registered to their sites, for example, accessing trial versions of products, or for buying goods online etc. In this scenario, the user is asked to register when they need to access some resources that need registration. To register, the user is provided a Registration form for creating username and password for that user. Once the user has given the inputs, the user navigates to a page where the user has to **personal information** and if the user is employed the **data** also has to be supplied by the user. Once the required data is provided by the user the user is registered and is informed of the success of registration. The scenario assumes that you will be creating the required data model for taking the login data (Person Entity), profile (Profile Entity) and professional (Profession Entity) data inputs from the user. [![WZ_usage_dm](../assets/WZ_usage_dm.png)](../assets/WZ_usage_dm.png)

## 1: Setup

is the set-up of an existing page - Getting Basic Details from the User for Registration with a button to invoke the Wizard to add Profile and Professional data.

- **a page** named to take the basic user data for Person entity.
- **Design** for the Page: use _Table_ to display/add/edit person details
- to invoke wizard to add profile and profession data - **event** should navigate to the wizard page (WizardBasic) which will be designed in the next step
- the App and give the inputs as needed.

[![wz_userregistrationpage](../assets/WZ_UserRegistrationPage.png)](../assets/WZ_UserRegistrationPage.png)

## 2: Basic Properties

1. **a Page** named in WaveMaker App
2. and Drop a wizard on the canvas. Once the Wizard is dropped onto the canvas, you will see the UI as shown below. By default only one step with the Title as Step Title is created. Note there are two action buttons – Cancel and Done respectively [![](../assets/WZ_usage_design.png)](../assets/WZ_usage_design.png)
3. the of the Step: Click on the step and in the properties panel change the Title to _Data_ [![](../assets/wz_usage_titleprops.png)](../assets/wz_usage_titleprops.png)
4. **More Steps to the Wizard**: Add one more step – click on the wizard canvas and click on **Step** Change Step to _Data_ by using the Title property of the step. [![](../assets/wz_usage_addsteps.png)](../assets/wz_usage_addsteps.png)

## 3: Design UI

**the UI for Personal Data Step:** Live Form bound to the Personal entity, using 3-column layout. [![WZ_usage_step1design](../assets/WZ_usage_step1design.png)](../assets/WZ_usage_step1design.png) ** UI for Professional Data Step**: Live Form bound to the Professional entity, using 1-column layout. [![WZ_usage_step2design](../assets/WZ_usage_step2design.png)](../assets/WZ_usage_step2design.png)

## 4: Event Configuration

- on the Wizard Step1 (Personal Data)
    - **Next**: Use Case – When the User is not Employed – On Blur Event of employed field In Personal Data Step when the user tabs out after entering a value in employed form field of Live Form On Blur event is fired. In the above use case, if the user does not wish to proceed to input Professional data as the user is not employed; then the appropriate handler has to be plugged into the On Blur of the employed field. This example has an On Blur JavaScript handler that does the following:
        
         = function($event, widget) {
        
        var employed = Page.Widgets.employed.datavalue;
        if (employed == "No")
        Page.Widgets.wizardstep2.enabledone = true;
        else
        Page.Widgets.wizardstep2.enabledone = false;
        };
        }
        \]);
        
    - the data value of the employed widget and assigns it to the employed variable.
    - the employed data value is “No” it enables the Done button in this step itself as the user can complete the registration in step 1 itself without going to step 2.
- Event on the Wizard Step 2 (Professional Data) – On Done:
    - Done: Use Case –When the User is Employed. In this case, the user is allowed to move to the next step to enter professional data. Once entered and Done button is clicked, On Done event fires. A JavaScript handler is added to On Done Event which does the following:
        
        1Done = function(widget, steps) {
        var liveData = Page.Widgets.liveform2.dataset.data;
        var ctrOfData = liveData.length;
        var profileData = Page.Widgets.liveform2.dataset.data\[ctrOfData -
        1\];
        var userName = profileData.personByPerson.userName;
        Page.Variables.UpdateRegistered.setInput('uid', userName);
        Page.Variables.UpdateRegistered.update();
        DialogService.open('alertdialog1', Page, {
        'mode': 'edit',
        'showInUserMode': true
        });
        };
        
    - the UserName from the Live Form Dataset
    - the UserName Input for the Update Query on the Person Service Variable to set the Registered field to true.
    - the service variable.
    - the Alert Dialog with Successful Message – Registration Successful – To create Alert Dialog and show up in a page – Refer Dialog Documentation
    - to Registration Details Page

## Run

- the app and click on Update Personal Data on User Registration page [![WZ_usage2_run1](../assets/WZ_usage2_run1.png)](../assets/WZ_usage2_run1.png)
- the Personal Details and click on NEXT to enter Professional Data [![wz_usage2_run2](../assets/WZ_usage2_run2.png)](../assets/WZ_usage2_run2.png)
- the app again and Enter the Personal Details with Employed set to NO, observe the DONE button with no navigation to Professional Data step [![WZ_usage_run1](../assets/WZ_usage_run1.png)](../assets/WZ_usage_run1.png)

- [2\. Container Widgets](/learn/app-development/widgets/widget-library/#container)
    - [2.1 Accordion](/learn/app-development/widgets/container/accordion/)
    - [2.2 Container](/learn/app-development/widgets/container/container/)
    - [2.3 Grid Layout](/learn/app-development/widgets/container/grid-layout/)
    - [2.4 Panel](/learn/app-development/widgets/container/panel/)
    - [2.5 Tabs](/learn/app-development/widgets/container/tabs/)
    - [2.6 Tile](/learn/app-development/widgets/container/tile/)
    - [2.7 Wizard](/learn/app-development/widgets/container/wizard/)
        - [Features](#features)
            - [Step Features](#step-features)
            - [Navigation](#navig)
            - [Widgets](#widgets)
        - [Usage Scenarios](#usage-scenarios)
            - [Step 1: Setup](#step1)
            - [Step 2: Properties](#step2)
            - [Step 3: UI Design](#step3)
            - [Step 4: Event Configuration](#step4)
            - [Test Run](#test-run)