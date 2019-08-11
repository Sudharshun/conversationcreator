# Speakeasy 

## What is Speakeasy?
An format for Defining Conversation Models using SPEAKING Model developed by Dell Hathaway Hymes.

## Why Speakeasy?
As Conversation Models evolve, I believe there is a need to evolve beyond the intent response paradigmn thats common in a lot of Assistant (Text to Speech) Systems. Smarter Conversations will begin to emerge once we model conversations on the same models that can be used to explain how humans converse.

## Introduction
TBD

## What are the types of data that can be Captured in Inquiries

(Partial Support for Ion Spec Types)

Type   | Supported across Instrumentalities  | Comments/Thoughts  
---|---|---
array| Web, Voice, Chat 
binary| Web, Voice,Chat 
boolean| Web, Voice,Chat 
date| Web, Voice,Chat 
datetime| Web, Voice,Chat 
decimal| Web, Voice,Chat 
duration| Web, Voice,Chat 
email| Web, Voice,Chat 
file| Web, Chat 
integer| Web, Voice,Chat 
link (limited supp)| Web, Chat 
number| Web, Voice,Chat 
object| Web, Voice,Chat | Generic Container element
set| Web, Voice,Chat |A non repeating set of elements
string| Web, Voice,Chat 
time| Web, Voice,Chat 
url| Web, Voice,Chat 

There is some great idea buried in Microsoft Adaptive Cards Actions as well , that today i believe loses some value by being too tightly coupled to UI actions. What if Actions can become more generic.

## Actions

Action.independentHttpAction(httpMethod, url, body, headers)

Action.managedFunction(managedSystemReference, FunctionName, callback, fallback)

Action.StartDialog (dialogReference, fallback, stimuli)

Action.OpenUrl(restricted to web and chat)

Action.SubmitDialog (to backend System,fallback, callback)

Action.SubmitDialogAndProgress(dialogReference- to progress to)

Action Should be defined as 

```
{
      "type": "independentHttpAction|managedFunction|StartDialog|OpenUrl|SubmitDialogAndProgress",
      "title": "Only allowed for not implicit|subtle",
      "method": :"only for independentHTTPAction|POST/GET",
      "managedSystemReference":"only For ManagedFuntion",
      "functionName":"only For ManagedFuntion",
      "callback":"dialog reference on success",
      "fallback":"dialog reference on failure",
      "dialogReference":"dialog to progress to / homage to Japanese Text Based Games"
      "stimuli":"what causes the action- ondatacapturecomplete|onbail|ontrigger(key,voice(fret))",
      "manifestation":"inquiry|callout(button)|childdialog",
      "actionsequence":"in the event of contention",
      "headers":"only for http",
      "endpoint":"where to send the action",
      "payload":"whats the payload for action(include references to elements"
}
```

### Sample Dialog JSON

```
{
    "id": "starterDialog1",
    "setting": "in the park",
    "motivation": "to make friends",
    "sequence": "friendly.conversation.001",
    "key": "millenial friendly",
    "instrumentalities": "Web|chat|voice",
    "norms": "TBD",
    "genre": "conversational|reasuring|fact finding",
    "elements": [
        {
            "id": "name",
            "type": "string",
            "title": "Name",
            "nature": "inquiry"
        },
        {
            "id": "email",
            "type": "email",
            "title": "Email",
            "nature": "inquiry"
        },
        {
            "id": "gender",
            "type": "string",
            "title": "Gender",
            "enum": [
                "male",
                "female"
            ],
            "nature": "inquiry",
            "default": "Male",
            "mutable": true,
            "required": true
        },
        {
            "id": "lookupnumber",
            "type": "string",
            "title": "Lookup Number",
            "actions": [
                {
                    "type": "Action.independentHttpAction",
                    "method": "POST",
                    "stimuli": "ondatacapture",
                    "headers": [
                        {
                            "name": "Authorization",
                            "value": ""
                        }
                    ],
                    "endpoint": "/validate",
                    "payload": "{'lookupnumber':'{{##value##}}'}"
                }
            ],
            "nature": "inquiry"
        },
        {
            "id": "legaldisc",
            "title": "disclosure",
            "type": "string",
            "value": "Content will be used to look up in our systems",
            "sequence": "last",
            "nature": "disclosure"
        }
    ],
    "actions": [
        {
            "type": "Action.managedFunction",
            "functionName": "pick.a.function.andrun",
            "stimuli": "ondatacapture",
            "title": "Submit",
            "manifestation": "callout",
            "managedSystemReference": "complexBackendSystem007",
            "payload": "{{#SELF#}}"
        }
    ]
}

```
