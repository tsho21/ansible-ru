# These are handlers that may be used within or outside this role.
#
#  Handlers are tasks that are called from antother task by the 'notify' directive.
#  These are akin to listenrs which get called when 'notify' fires.
#  'notify' fires only when the calling task makes a change:
#
#  Task A creates a firewalld port opening 443, has 'notify' on handler 'restart-firewalld'.
#  Handler 'restart-firewalld' will only execute when 'notify' fires.
#  Task A will ONLY fire 'notify' to its handlers when it actually makes the 443 port change.
#   - IE. if the port change is already present, it will make no change and thus 'notify' does not fire.
