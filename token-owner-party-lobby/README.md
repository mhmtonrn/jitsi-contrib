# Token Owner Party

This plugin prevents the unauthorized users to create a room and terminates the
conference when the owner leaves. It's designed to run with `token_verification`
and `token_affiliation` plugins.

## Installation

- Copy this script to the Prosody plugins folder. It's the following folder on
  Debian

  ```bash
  cd /usr/share/jitsi-meet/prosody-plugins/
  wget -O mod_token_owner_party.lua https://raw.githubusercontent.com/mhmtonrn/jitsi-contrib/main/token-owner-party-lobby/mod_token_owner_party_lobby.lua
  ```

- Enable module in your prosody config.

  _/etc/prosody/conf.d/meet.mydomain.com.cfg.lua_

  ```lua
  Component "conference.meet.mydomain.com" "muc"
    modules_enabled = {
      ...
      ...
      "token_verification";
      "token_affiliation";
      "token_owner_party_lobby";
    }
    party_check_timeout = 20
  ```

- For most scenarios you may want to disable auto-ownership on Jicofo.

  ```bash
  hocon -f /etc/jitsi/jicofo/jicofo.conf \
      set jicofo.conference.enable-auto-owner false
  ```

- Restart the services

  ```bash
  systemctl restart prosody.service
  systemctl restart jicofo.service
  ```