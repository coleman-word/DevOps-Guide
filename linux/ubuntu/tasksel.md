# Tasksel

## NAME
       tasksel - a user interface for installing tasks

## SYNOPSIS
       tasksel install <task>

       tasksel remove <task>

       tasksel [options]

## DESCRIPTION
       tasksel shows all available tasks and allows to user to select ones to
       install

OPTIONS
       -t, --test
           test mode; don't actually install or remove packages

       --new-install
           automatically select some tasks without even displaying them to the
           user; default other tasks to on; used during new Debian installs.

       --list-tasks
           list on stdout the tasks that would be displayed in the tasksel
           interface

       --task-packages task
           lists on stdout the packages that are available and part of the
           given task

           Note that this option may be given more than once.

       --task-desc task
           outputs the extended description of the given task

     --debconf-apt-from waypoint
           Start the debconf-apt-progress bar here.

       --debconf-apt-to waypoint
           End the debconf-apt-progress bar here.

       --debconf-apt-progress options
           Pass the specified options to the debconf-apt-progress command that
           tasksel runs. These will be appended to any --from and --to options
           constructed by tasksel itself based on --debconf-apt-from and
           --debconf-apt-to options.




