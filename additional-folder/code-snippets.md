# Here I would copy/paste code chunks I've been working on at codepen and I don't want to lose or keep a single codepen just for that.

### code from FCC Twitch Zipline I've been working on:

```javascript
$(document).ready(function() {

  var twitchAPI = "https://api.twitch.tv/kraken/streams/"; // URL for TWITCH API for streams

  var twitchUser = "https://api.twitch.tv/kraken/users/"; // URL for TWITCH API for users

  var userNotFound = "http://www-cdn.jtvnw.net/images/xarth/404_user_50x50.png"; // User not found logo

  var userArray = ["freecodecamp", "GeoffStorbeck", "terakilobyte", "habathcx", "RobotCaleb", "thomasballinger", "noobs2ninjas", "beohoff", "medryBW"]; // Array of users

  userArray.forEach(function(element) {

      $.getJSON(twitchAPI + element, function(data) {

          //Take action if the stream is offline
          if (data.stream == null) {
            $.getJSON(twitchUser + element, function(datauser) {
              //if user has a logo display logo
              if (datauser.logo) {
                //Create a table row for each user with user avatar, and user name
                var li = "<a href='http://www.twitch.tv/" + datauser.name + "' target='_blank' class='twitch_link'><li>";
                li += "<img src=" + datauser.logo + " alt='logo del stream' class='user_image'/>";
                li += "<span class='username'>" + datauser.name + "</span>";
                li += "</li></a>";
                $('ul').append(li);
              }
              //if user does not have a logo display logo for 404_user_not_found
              else {
                //Create a table row for each user with user avatar, and user name
                var li = "<a href='http://www.twitch.tv/" + datauser.name + "' target='_blank' class='twitch_link'><li>";
                li += "<img src=" + userNotFound + " alt='logo del stream' class='user_image'/>";
                li += "<span class='username'>" + datauser.name + "</span>";
                li += "</li>";
                $('ul').append(li);
              }
              console.log("Stream is offline"); // Test 
            });
            //Take action if the stream is online
          } else {

            //Create a table row for each user with user avatar, user name, game name, and user status
            var li = "<a href='" + data.stream.channel.url + "' target='_blank' class='twitch_link'><li>";
            li += "<img src=" + data.stream.channel.logo + " alt='logo del stream' class='user_image'/>";
            li += "<span class='username'>" + data.stream.channel.display_name + "</span>";
            li += "<span class='channel_game' class=''>" + data.stream.game + "</span><br/>";
            li += "<span class='channel_status' class='small'>" + data.stream.channel.status + "</span>";
            li += "</li>";
            $('ul').append(li);

            console.log(data.stream.channel.display_name); // Test 
            console.log(data.stream.game); // Test 
            console.log(data.stream.channel.status); // Test 
          }

        }) //end of getJSON
    }) //end of foreach

}) //End of document.ready
```
