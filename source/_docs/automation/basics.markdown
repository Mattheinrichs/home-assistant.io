---
title: "Understanding automations"
description: "A breakdown of what an automation consists of."
---

All {% term automations %} are made of at least a {% term trigger %} and an {% term action %}. Optionally combined with a {% term condition %}. Take for example the automation:

> When Paulus entered home and if the sun after sunset, then do: turn the lights on in the living room.

## Parts of an automation

We can break up the previous automation example into the following three parts:

```text
(trigger part)    When Paulus entered home
(condition part)  And if the sun after sunset
(action part)     Then do: turn on the lights in the living room
```

Each part has a target. The target can be an {% term entity %}, a {% term device %}, a {% term service %} or a group of them. You can see examples in the following sections.

### Trigger part

The [trigger](/docs/automation/trigger/) belongs to the first part of the automation. An automation must have at least one trigger, related to a target. When the trigger part is verified, the automation starts. In the example of the automation above, the trigger part _When Paulus entered home_ has:

- the target: _Paulus_.
- the trigger: _entered home_.

A person entering home can be tracked in Home Assistant using {% term devices %}/{% term sensors %}, that observes the state of Paulus changing from `not_home` to `home`.

### Condition part

The second part of an automation has the [condition](/docs/automation/condition/). Conditions are optional tests directed to a target that can limit an automation to only work in specific cases. A condition will be tested against the current state of the system. This includes the current time, devices, people and other things like the sun. In the example of the automation above, the result of the automation will be verified only if the sun has set.

The condition part _And if the sun after sunset_ has:

- the target: _sun_.
- the condition: _sun after sunset_.

{% note %}
The difference between a trigger and a condition can be confusing as they are very similar.

Triggers require an event to happen for the conditions to be evaluated using current state information.

Event: Arrive home \
Condition: After Sunset? \
Action: Turn lights on

{% endnote %}

### Action part

The last part of an automation has the [action](/docs/automation/action/). The action part will be performed only if the trigger and condition parts are met. The action part can be turn a light on, set the temperature on your thermostat or activate a scene. An automation must have at least one action, related to a target.

The action part _Then do: turn on the lights in the living room_ has:

- the target: _lights in the living room_.
- the action: _turn on_.

## Exploring the internal state

Automations interact directly with the internal state of Home Assistant, so you'll need to familiarize yourself with it. Home Assistant exposes its current state via the developer tools. These are available at the bottom of the sidebar in the frontend. {% my developer_states title="**Settings** > **Developer tools** > **States**" %} will show all currently available states. An entity can be anything. A light, a switch, a person and even the sun. A state consists of the following parts:

| Name | Description | Example |
| ---- | ----- | ---- |
| Entity ID | Unique identifier for the entity. | `light.living_room` |
| State | The current state of the device. | `off` |
| Attributes | Extra data related to the device and/or current state. | `brightness` |

State changes can be used as the source of triggers and the current state can be used in conditions.

To explore the available _actions_, open the {% my developer_services title="**Settings** > **Developer tools** > **Actions**" %}. _Actions_ allow changing anything. For example, turn on a light, run a script, or enable a scene. Each _action_ has a domain and a name. For example, the _action_ {% my developer_call_service service="light.turn_on" %} is capable of turning on any light in your system. Parameters can be passed to an _action_ to indicate, for example, which device to activate or which color to use.

## Creating automations

Now that you've got a sneak peek of what is possible, it's time to get your feet wet and create your first automation.

By default, to create automations, use the [automation editor](/docs/automation/editor/).

### Creating automations with the new Labs features

{% include integrations/labs_entity_triggers_note.md %}

After enabling the automation preview features in Labs, you can create an automation in the visual editor of the UI by following the steps below.

1. Go to **Settings** > **Automations & scenes**.
2. In the lower right corner, select **Create automation** > **Create new automation**.

#### Adding a trigger

1. In the **When** section, select **Add trigger**.
2. Now you can do one of the following:
   - Select a target and then a trigger.
     1. Under **By target**, select the entity, device or service to which you want to apply the trigger to. You can find the available entities, devices or services listed by:
        - Area of your home, in the **Home** section.
        - **Entities**, **Devices** and **Services**, in the **Unassigned** section.
        - Labels that you have previously created, in the **Labels** section.
     2. For that target, you can see the available triggers on the right side. Select **+** on the desired one.
   - Select a trigger.
     1. Select **By type**, and then select the trigger type from the list on the left.
     2. From the listed triggers, select **+** on the one you choose.
   - Search for a trigger or target and then select a trigger.
     1. Enter the name of one of the following in the search box:
        - A target: an entity, a device or a service.
        - A group of targets: an area or label.
        - A trigger.
     2. From the listed results, select **+** on the desired trigger.
3. In the window on the right, you will have different options depending on the selected trigger. You might find the following ones, for example:
   - Under **Targets**, you can select the first target or another one by selecting **Add target**.
     1. Do one of the following:
        - Select an entity, device or service to monitor a specific one.
        - Select entities, devices or services in an area, floor or with a certain label to monitor a group of them.
     2. You can add more targets by selecting **Add target** again.
   - Under **Behavior**, you can decide how the automation starts by selecting one of the options there.
     - **First**: if monitoring multiple targets, the automation only fires on the first time the trigger is verified for a target.
     - **Last**: if monitoring multiple targets, the automation only fires after the trigger is verified for all targets.
     - **Any**: the automation fires whenever a trigger of a monitored target is verified.
4. Select **Save**.

#### Adding a condition

Note that you don´t need to add a condition to create an automation.

1. In the **And if** section, select **Add condition**.
2. Under **Blocks**, you have the following options:
   - If you want to make sure that a condition is not verified for the automation to run, select  **+** on the **Not** block.
   - If you will add more than one condition, you can select:
     - the **And** block to make sure all conditions are verified for the automation to run.
     - the **Or** block to make sure at least one of the conditions is verified for the automation to run.
3. Select **Add condition** again and now you can:
   - Select a target and then a condition.
     1. Under **By target**, select the entity, device or service to which you want to apply the condition to. You can find the available entities, devices or services listed by:
        - Area of your home, in the **Home** section.
        - **Entities**, **Devices** and **Services**, in the **Unassigned** section.
        - Labels that you have previously created, in the **Labels** section.
     2. For that target, you can see the available conditions on the right side. Select **+** on the desired one.
   - Select a condition.
     1. Select **By type**, and then select the condition type from the list on the left.
     2. From the listed conditions, select **+** on the one you choose.
   - Search for a condition or target and then select a condition.
     1. Enter the name of one of the following in the search box:
        - A target: an entity, a device or a service.
        - A group of targets: an area or label.
        - A condition.
     2. From the listed results, select **+** on the desired condition.
4. In the window on the right, you will have different options depending on the selected condition. Under **Targets**, you can add the first target or another one by selecting **Add target**.
   1. Do one of the following:
      - Select an entity, device or service to monitor a specific one.
      - Select entities, devices or services in an area, floor or with a certain label to monitor a group of them.
   2. You can add another target by selecting **Add target** again.
5. Select **Save**.

#### Adding an action

1. In the **Then do** section, select **Add action**.
2. Under **Blocks**, you have many options that allow you, for example, to:
   - Set up conditions for specific actions.
   - Define the way a sequence of actions is performed.
   - Wait for a trigger or a template to run a sequence of actions.
3. Now you can do one of the following:
   - Select a target and then an action.
     1. Under **By target**, select the entity, device or service to which you want to apply the action to. You can find the available entities, devices or services listed by:
        - Area of your home, in the **Home** section.
        - **Entities**, **Devices** and **Services**, in the **Unassigned** section.
        - Labels that you have previously created, in the **Labels** section.
     2. For that target, you can see the available actions on the right side. Select **+** on the desired one.
   - Select an action.
     1. Select **By type**, and then select the action type from the list on the left.
     2. From the listed actions, select **+** on the one you choose.
   - Search for an action or target and then select an action.
     1. Enter the name of one of the following in the search box:
        - A target: an entity, a device or a service.
        - A group of targets: an area or label.
        - An action.
     2. From the listed results, select **+** on the desired action.
4. In the window on the right, you will have different options depending on the selected action. Under **Targets**, you can add the first target or another one by selecting **Add target**.
   1. Do one of the following:
      - Select an entity, device or service to monitor a specific one.
      - Select entities, devices or services in an area, floor or with a certain label to monitor a group of them.
   2. You can add another target by selecting **Add target** again.
5. Select **Save**.
