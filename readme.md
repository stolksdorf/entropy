# entropy

A highly opinionated electron music player



## features
- Dynamic playlists with code
- Global keyboard shortcuts
- Chromecast audio support
- Able to handle streamed music (youtube, soundcloud, etc.)
- Configs all through JSON
- 'Up next' playlist
- Menu and shortcuts configured from JSON file
- Use CSS grids for layout, https://github.com/electron/electron/issues/4565
- remember layout and music selection between sessions

### streamed music

- Stored as a separate JSON
- Store the entries exactly like what is generated from library generation
- Easily download and add to library
- Maintain the metadata: playcount, any classifications
-


### tags & metadata
- in the config, have a list of tags (with associated colors). use mood
  - intense
  - no vocals
  - calm
  - concentration
  - upbeat
- Able to edit the metadata directly
- Tags fields we need
  - Date added to Entropy
  - Unique ID to entropy? (probably not needed)
  - Playcount?
  - mood
  - last played


### playlists
[Intersting playlsit idea](http://universalplaylist.stavros.io/)
- Each playlist is it's own js file
- Have a few static playlists (All, Up next)
- Expose some utils, duration, last_played, etc.

```javascript
module.exports = {
	name : 'test playlist',
	songs : {
		"47314f0a-46f5-4e07-b094-567cfba906bb" : "Shawn Wasabi - Spicy Boyfriend",
		"199cc472-ecfa-45ca-85fd-b0033c13cc9b" : "The Neighbourhood - Daddy Issues"

	},

	code : (songs)=>{
		return _.chain(songs)
			.filter((song)=>song.duration < 5 * MINUTES)
			.sortBy((song)=>song.dateAdded)
			.take(25)
			.value()
	}
}
```
- static Playlists: All, Stream, Up next, search



### Actions
- change play mode: shuffle, single repeat.
- play/pause
- next/previous
- add to up_next
- rescan library
- recalculate playlists
- Open playlist from edit
- open settings for edit
- init
- set active playlist
- create playlsit
- delete song (?)
- modify mood

### extra screens
- Search
- Song editor
- History of events?
- chromecast
- playlist view
-


### settings

```javascript
{
	"library" : ["C:/Dropbox/root/Programming/Javascript/entropy/test_lib"],

	"shortcuts" : {
		"global": {
			"CommandOrControl+X" : "play",
			"CommandOrControl+Y" : "pause",
			"CommandOrControl+Z" : "next"
		},
		"local" : {
			"CommandOrControl+R" : "rescan",
			"CommandOrControl+L" : "mode:repeat"
		}
	},

	"moods" : {
		"intense" : "#e74c3c",
		"no_vocals": "#bdc3c7",
		"calm" : "#1abc9c",
		"concentration" : "#8e44ad"
		"upbeat" : "##f1c40f"
	}
}
```


### search
- basic search using title and artist
- using colons will add property access, eg. `mood:calm`, `title:fancy`


### desings

http://media02.hongkiat.com/music-app-mobile-designs/2-music-app-designs-for-mobile.jpg
http://media02.hongkiat.com/music-app-mobile-designs/14-music-app-designs-for-mobile.jpg