---
layout: project
type: project
image: images/commissioning tool images/v3/commissioning_tool_config_v3_inclinometer_input.png
title: Commissioning Tool UI Wireframes
permalink: projects/commissioningtoolwireframe
# All dates must be YYYY-MM-DD format!
date: 2021-12-15
labels:
  - User Interface
  - Wireframe
summary: Progressioning of a project for which I designed and programmed the frontend. This is the UI development.
---

I had been tasked with developing the frontend to software that connects with hardware and allows someone off-site to check certain readings, adjust offsets for measuring-hardware based on feedback from an on-site engineer (who manually confirms measurements), view graphs of the different measuring-hardwares' performance, and adjust thresholds on said graphs as necessary. As the project progressed, features were added, removed, or tweaked, thus my wireframes took on very different forms. I was on a team of two: @alex-wells on the backend/API and me on the frontend. I created these wireframes in Pencil, and I will cover development and the live User Interface in another entry.

## Version 1
In this phase, I had been given an extra feature, Firmware, that did not make it into subsequent versions, as it was unneccessary and would not add value for the user, as it would simply be extraneous.

At this early stage, trying to visualise how things would come together on the interface was important, so we could consider how the user would interact, if there was an appropriate order based on a usual commissioning session, and whether the infomation would be apparent.

<div class="ui large centered rounded images">
  <img class="ui image" src="../images/commissioning tool images/v1/commissioning_tool_config_home.png">
  <img class="ui image" src="../images/commissioning tool images/v1/commissioning_tool_config_firmware_version.png">
<img class="ui image" src="../images/commissioning tool images/v1/commissioning_tool_config_firmware_update.png">
<img class="ui image" src="../images/commissioning tool images/v1/commissioning_tool_config_voltage_and_readings.png">
</div>

## Version 2
In the second iteration, the unnecessary firmware check and updated the layout for the input/button pairs for the manually inputting an offset to the hardware. I wanted a visual indicator of some sort to show the user had submitted the manual reading from the commissioning engineer to calculate the offset within the hardware, but I was not quite sure what that would entail at this point, hence the checkboxes as a temporary visual indicator that calculation had been successful.

I wanted an indicator that showed that inputted readings on the inclinometer offsets were bound within a range, shown as green or red highlights on the wireframe (in production, there will only be a highlight at all if you are outside the range). I also tried to indicate the possibility that parts of the page would be disabled until certain tasks were completed, though this would not be the case as the project progressed.

A global submit button was further introduced at the bottom of the page. The inclinometer calculation buttons would submit back to the API, then the global submit would save the changes in configuration back to the hardware. This concept of submitting certain information to the API, rather than directly to the hardware, would be better fleshed out at a later time.

<div class="ui large centered rounded images">
  <img class="ui image" src="../images/commissioning tool images/v2/commissioning_tool_config_v2_home.png">
  <img class="ui image" src="../images/commissioning tool images/v2/commissioning_tool_config_v2_connected.png">
<img class="ui image" src="../images/commissioning tool images/v2/commissioning_tool_config_v2_volts.png">
<img class="ui image" src="../images/commissioning tool images/v2/commissioning_tool_config_v2_volts_submit.png">
<img class="ui image" src="../images/commissioning tool images/v2/commissioning_tool_config_v2_inclinometer_input.png">
<img class="ui image" src="../images/commissioning tool images/v2/commissioning_tool_config_v2_inclinometer_input_ready.png">
<img class="ui image" src="../images/commissioning tool images/v2/commissioning_tool_config_v2_inclinometer_input_submitted.png">
</div>

## Version 3
As I worked more on the software and realised some of its capabilities, I considered more hiding/showing of sections, rather than disabling them. This carried into the final stages of the project, as you will see. 

In this iteration, I added in visual feedback for the inclinometer readings using labels (the label wording will change in the end). The first is the reading from the hardware, the second is what is entered in the input box (reflecting the manual measurements reported by an on-site engineer), and the last is the calculated offset (which is found automatically, as the frontend performs a calculation using a raw measurement from the hardware and the inputted reading as entered by the user). Once calculate is pressed, the calculation is performed and the result is both displayed to the user and saved to the API.

At this stage, the visual indicators (checkboxes) remained in the wireframe, but not the actual product, as I believe the visual feedback from the measurements and calculations would be enough. Finally, the global submit button was moved to the side, rather than below, as I shifted the entire layout. Again, the submit button would save any changes the user had inputted back to the hardware.

<div class="ui large centered rounded images">
  <img class="ui image" src="../images/commissioning tool images/v3/commissioning_tool_config_v3_home.png">
<img class="ui image" src="../images/commissioning tool images/v3/commissioning_tool_config_v3_site_selection.png">
  <img class="ui image" src="../images/commissioning tool images/v3/commissioning_tool_config_v3_connected.png">
<img class="ui image" src="../images/commissioning tool images/v3/commissioning_tool_config_v3_get_voltage.png">
<img class="ui image" src="../images/commissioning tool images/v3/commissioning_tool_config_v3_inclinometer_input.png">
<img class="ui image" src="../images/commissioning tool images/v3/commissioning_tool_config_v3_inclinometer_calculation.png">
<img class="ui image" src="../images/commissioning tool images/v3/commissioning_tool_config_v3_inclinometers_submitted.png">
</div>

## Version 4
In this final wireframe, the most complex part of the project got added in, which was a channel select and display area. This would allow the off-site engineer to view the signals from various channels which correspond to hardware. Monitoring this allows for early prediction of hardware failure, so an engineer can be sent to perform preventative maintenence or to schedule an engineer in the near future, or notice already faulty components, so an engineer could appropriately replace them. 

As I felt the labels added as visual feedback on the inclinometer input/button pairings would be sufficient, I removed the checkbox placeholders from the wireframe. The label wording was also adjusted to be more apparent to the user what is being shown.

I used the negative space on the right side of the tool to display the channel dropdown, which allows the user to choose which signals to display. The refresh button pulls the latest two profiles from the hardware, and each include the channel name, position (raise, lower, hunting), and a timestamp at the top. The x axis is time (seconds) and the y axis changes with each channel, reflecting the unit of measurement the hardware uses. Each chart has a padding of 10% above and below the displayed signals, so the chart is easy to read (no line is either at the top or bottom border). 

Some channels have a threshold, which the off-site engineer can adjust using an input/button pair. The allowable values for such are within 10% of either side of the range, so each channel that has a threshold have different min/max, which are calculated automatically within the tool.

Just as with the calculate buttons on the inclinometer side, the threshold set button submits the value back to the API, and the global submit button (bottom) submits it to the actual hardware. I added visual feedback messages to the global submit button showing either that no new information had been submitted (in the case no new inclinometer measurements or thresholds were inputted) or that the configuration was successfully saved to the hardware with a timestamp. 

<div class="ui large centered rounded images">
  <img class="ui image" src="../images/commissioning tool images/v4/commissioning_tool_config_v4_home.png">
<img class="ui image" src="../images/commissioning tool images/v4/commissioning_tool_config_v4_site_selections.png">
  <img class="ui image" src="../images/commissioning tool images/v4/commissioning_tool_config_v4_connected.png">
<img class="ui image" src="../images/commissioning tool images/v4/commissioning_tool_config_v4_get_voltage.png">
<img class="ui image" src="../images/commissioning tool images/v4/commissioning_tool_config_v4_inc_offsets_input.png">
<img class="ui image" src="../images/commissioning tool images/v4/commissioning_tool_config_v4_inc_offsets_calculate.png">
<img class="ui image" src="../images/commissioning tool images/v4/commissioning_tool_config_v4_channel_select.png">
<img class="ui image" src="../images/commissioning tool images/v4/commissioning_tool_config_v4_channel_refresh.png">
<img class="ui image" src="../images/commissioning tool images/v4/commissioning_tool_config_v4_channel_set_threshold_1.png">
<img class="ui image" src="../images/commissioning tool images/v4/commissioning_tool_config_v4_channel_set_threshold_2.png">
<img class="ui image" src="../images/commissioning tool images/v4/commissioning_tool_config_v4_global_submit.png">
</div>