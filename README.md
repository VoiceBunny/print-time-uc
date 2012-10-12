#Instructions

Read carefully the following use case description and implement it using the programming language of your choice.
When you are ready, **send us** an email to wanted@voicebunny.com with you resumé and a url where we can check your solution.

# Print Time UC

### Context of Use

VoiceBunny needs to display time and date to any visitor. If possible, that data should be displayed in the visitor's computer's local time format.

### Stakeholders and Interests

***Visitor:** To be able to see accurate times and dates.

**Merrcury:** To let visitors know when a date has been rendered using the local time of the computer.

### Success Guarantees

The time and date are printed in the local time of the computer.

### Triggers

0100 - A user requests that SuD(System under Development) return an interface that requires times to be displayed.

### Main Scenario

- 0100 - Trigger

- 0200 - SuD determines the local time of the browser (<code>$Browser.LocalTime</code>), and compares it with GMT (<code>$Browser.GMTOffset</code>)

- 0300 - SuD compares <code>$Browser.LocalTime</code> and <code>$Browser.GMTOffset</code> to real the GMT time provided by the server (<code>$Server.GMTTime</code>)

    <code>$Discrepancy = ($Browser.LocalTime + $Browser.GMTOffset) - $Server.GMTTime</code>

    For example, if GMT is 11:47, browser time is 16:45, and browser GMT offset is -300 minutes

    <code>$Discrepancy = ( 16:45 + (-300 min) ) - 11:47 = 11:45 - 11:47 = -2 minutes</code>

- 0400 - SuD validates that the absolute value (abs) of the discrepancy is not more than 5 minutes.

- 0500 - SuD finds the time to be rendered <code>$Time.Render = $Time.InGMT - $Browser.GMTOffset</code>

    For example, if the time to be printed is 2008/07/04 14:46:00 GMT

    <code>$Time.Render = 2008/07/04 14:46:00 - (300 minutes) = 2008/07/04 09:46:00</code>

- 0600 - SuD prints the time as the current locale configuration without referring to any time zone, and adding the symbol * after the time (without leaving a blank space)

- 0700 - SuD prints at the bottom of the page a disclaimer.

### Extensions

#### E 0200a
If SuD cannot determine the local time or its GMT offset:
    
- 0100 - SuD prints the time in GMT, adding the word " GMT" at the end of the time. UC ends.

#### E 0400a
If the discrepancy is more than 5 minutes:
    
- 0100 - SuD prints the time in GMT, adding the word " GMT" at the end of the time. UC ends.
