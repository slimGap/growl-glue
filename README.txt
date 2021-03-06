== DESCRIPTION:

Simplifies Growl configuration for Autotest.

== Autotest Features:

* Easy configuration of growl notifications in ~/.autotest
* Comes bundled with sample green/red images, or you can supply your own
* Ability to specify OS X speech options (e.g. "Oh No!", if test failure)
* Ability to use a different OS X voice for each status
* Ability to specify sounds for success or failure conditions
* Ability to color code the Growl display for success, pending, and failure
* RSpec support
* Test::Unit support

== Autotest Growl Integration:

The Autotest growl configuration should happen in ~/.autotest. To get up and running very quickly with basic notifications + images:

  require 'growl_glue'
  GrowlGlue::Autotest.initialize

  
If you wish to customize, further, you simply need to supply your own block, to which the GrowlGlue configuration object will be passed:

  require 'growl_glue'
  GrowlGlue::Autotest.initialize do |config|
    ...
  end

It is recommended that you use network notifications due to a bug in Growl on OS X 10.5. Inside of the Growl Preferences pane, on the Network tab, make sure the "Listen for incoming notifications" checkbox is checked, and then *restart Growl*.  Then configure GrowlGlue inside of the setup block:

  config.notification :use_network_notifications => true

OS X Speech:

  config.say   :pending => "Almost there guy!"
  config.voice :pending => "Boing"

  config.say   :failure => "PANIC PANIC PANIC"
  config.voice :failure => "Hysterical"

Audio Notifications:

If you have *OS X 10.5* -or- *sndplay* compiled and in the path, you can have different sounds played based on test success or failure.  The "location" below is optional, as it defaults to "/System/Library/Sounds":

  config.sound :success => "Glass.aiff"
  config.sound :pending => "Glass.aiff"
  config.sound :failure => "Basso.aiff"
  config.sound :location => "/System/Library/Sounds/" (optional)


Color Code Growl:
Growl allows you to apply different styles based on an alert's 'importance' (System Preferences > Growl > Display Options). This allows you to extend the red/yellow/green pattern to the Growl display.

  GrowlGlue automatically sets the following levels of importance:
    success = 'Moderate'
    pending = 'High'
    failure = 'Emergency'

It is recommended that you use 'Normal' for other Growl alerts.
  
GrowlGlue comes with success and error images it will use on test success and error, respectively. If you wish to supply your own, for example:

  config.image :success => "~/Library/autotest/success.png"
  config.image :pending => "~/Library/autotest/pending.png"
  config.image :failure => "~/Library/autotest/failure.png"

By default, "Tests Passed" and "Tests Failed" will be used as the growl titles. You can supply your own, though:

  config.title :success => "Love", :failure => "Hatred", :pending => "Well, OK!"

As an example, this is what I normally use:

  GrowlGlue::Autotest.initialize do |config|
    config.notification :use_network_notifications => true
  
    config.sound :success => "Glass.aiff"
    config.sound :pending => "Glass.aiff"
  
    config.say   :failure => "PANIC PANIC PANIC"
    config.voice :failure => "Hysterical"
    config.sound :failure => "Basso.aiff"
  end


== REQUIREMENTS:

* Growl 1.1.4 (may work on previous versions but not tested)
* Growlnotify Extra installed
* Note: you may reference "this video":http://growl-glue.rubyforge.org/files/InstallingGrowlNotify.mov to illustrate how to install growlnotify.

== OPTIONAL:

* sndplay for #sound notification (only needed outside of OS X 10.5).  If anyone can tell me if earlier versions of OS X have *afplay* please let me know.

== INSTALL:

* sudo gem install growl-glue
* Download Growl from http://growl.info
* After installing Growl, install the Growlnotify Extra included in the DMG
* After Growl is installed, configure your ~/.autotest file as described above

== BUGS / ISSUES:

Please let me know if you encounter any issues.  You can also follow or fork development on the github project:

http://github.com/nimbletechnique/growl-glue/tree/master

== AUTHORS

* Collin VanDyck <collin@nimbletechnique.com>

== OTHER

If you use my gem, and like it, it would be great to get a recommendation on Working with Rails:

http://workingwithrails.com/recommendation/new/person/13224-collin-vandyck.

Thanks!

== LICENSE:

(The MIT License)

Copyright (c) 2008 Nimble Technique, LLC

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
