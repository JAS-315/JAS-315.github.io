---
layout: project
type: project
image: images/commissioning tool images/v3/commissioning_tool_config_v3_inclinometer_input.png
title: Commissioning Tool UI
permalink: projects/commissioningtool
# All dates must be YYYY-MM-DD format!
date: 2021-12-15
labels:
  - User Interface
  - Wireframe
summary: Progressioning of a project for which I designed and programmed the frontend. This is the UI development.
---

I had been tasked with developing the frontend to software that connects with hardware and allows someone to check certain readings, adjust offsets for measuring-hardware based on feedback from an on-site engineer (who was manually confirming measurements), view graphs of the different measuring-hardwares' performance, and adjust thresholds on said graphs as necessary. As the project progressed, features were added, removed, or tweaked, thus my wireframes took on very different forms. I was on a team of two: NAME on the backend and me on the frontend. I created these wireframes in Pencil, and I will cover development and the live User Interface in another entry.

## Version 1
In this phase, we had been given an extra feature, Firmware, that did not make it into subsequent versions, as it was unneccessary and would not add value for the user, as it would simply be extraneous.

At this early stage, trying to visualise how things would come together on the page was important, so we could consider how the user would interact, if there was an appropriate order based on a usual commissioning session, and whether the infomation would be apparent.

<div class="ui large centered rounded images">
  <img class="ui image" src="../images/commissioning tool images/v1/commissioning_tool_config_home.png">
  <img class="ui image" src="../images/commissioning tool images/v1/commissioning_tool_config_firmware_version.png">
<img class="ui image" src="../images/commissioning tool images/v1/commissioning_tool_config_firmware_update.png">
<img class="ui image" src="../images/commissioning tool images/v1/commissioning_tool_config_voltage_and_readings.png">
</div>

## Version 2
In the second iteration, the unnecessary firmware check and updated the layout for the input/button pairs for the manually inputting an offset to the hardware. I wanted a visual indicator of some sort to show the user had submitted the manual reading from the commissioning engineer to calculate the offset within the hardware, but I was not quite sure what that would entail  at this point, hence the checkboxes as a temporary visual indicator. 

I wanted an indicator that showed that inputted readings on the inclinometer offsets were bound within a range, shown as green or red highlights on the wireframe (in production, there will only be a highlight at all if you are outside the range). I also tried to indicate the possibility that parts of the page would be disabled until certain tasks were completed, though this would not be the case as the project progressed.

A global submit button was further introduced at the bottom of the page. The inclinometer submission buttons submit back to the API, then the global submit would save the changes in configuration back to the hardware.

<div class="ui large centered rounded images">
  <img class="ui image" src="../images/commissioning tool images/v2/commissioning_tool_config_v2_home.png">
  <img class="ui image" src="../images/commissioning tool images/v2/commissioning_tool_config_v2_connected.png">
<img class="ui image" src="../images/commissioning tool images/v2/commissioning_tool_config_v2_volts.png">
<img class="ui image" src="../images/commissioning tool images/v2/commissioning_tool_config_v2_volts_submit.png">
<img class="ui image" src="../images/commissioning tool images/v2/commissioning_tool_config_v2_inclinometer_input.png">
<img class="ui image" src="../images/commissioning tool images/v2/commissioning_tool_config_v2_inclinometer_input_ready.png">
<img class="ui image" src="../images/commissioning tool images/v2/commissioning_tool_config_v2_inclinometer_input_submitted.png">
</div>

