# subDlTrigger

This is a small ruby script intended to be used to automate deluge (and
similar tools which use same interface) to trigger automatic download of
subtitles immedietly after file is downloaded.

## Requirements 

 * Ruby 1.8.7 or greater (tested only on 1.8.7 series)
 * Either or both:
  * subliminal [1] - https://github.com/Diaoul/subliminal
  * periscope - http://code.google.com/p/periscope/

In order to enable proper languages to be dowloaded by either of the clients,
you must create a configuration file for these tools.  See [1] for more
details.


## Installation

 * Clone the project via git:
     git clone git://github.com/rasjani/subdltrigger.git
     cd subdltrigger
 * You can either copy the script to some folder where your torrent client can
   execute it. Or in order to make updates a breeze, just symlink it from the 
   git repo:
     sudo ln -s ./subdltrigger /usr/local/bin
 * Install and configure your chosen subtitle downloader.
 * Configure deluge to use subdltrigger when download finishes, more detailed
   instructions in your torrent client manual, but things go like this:

  * Enable "execute" plugin
  * In "execute" plugin preferences, add "Torrent Added" event and use
    "/usr/local/bin/subdltrigger" as command.

## How things work

Script gets 3 parameters, no more no less. First one is torrent hash which is
not used for anything, second is the filename or directory and third parameter
is the download folder where the previous file/directory reasides. 

When subdltrigger starts, it autoscans which tool can be found in the PATH
environment and automatically uses the first occurance. If no tools cannot be
found, script will exit with exitcode 1.

Then, subdltrigger scans the files in order to isolate video files (matching
happens only via file extension) and then triggers a call to appropriate
downloader. 

subdltrigger relies that downloader supports configuration files which define
what services to use and what languages to download.

## Notes

 [1] - At the time of writing this, subliminal does not support external
configuration file. Patches have been submitted but they are still pending to
be merged to upstream.  See pullrequest:
https://github.com/Diaoul/subliminal/pull/138
