## How to open the last URL using clipmenu-url.

NOTE: You should have clipmenu installed and setup, in case you don't.
https://www.youtube.com/watch?v=vi_Z-5VC_sQ this is a link tomy video on how to setup clipmenu.

1. Creat a file and clipmenu-url, you can name it whatever you want.

`$ sudo touch /usr/bin/clipmenu-url`

2. Copy the script to clipmenu-url and save the file.

`$ sudo vim /usr/bin/clipmenu-url`

	#!/usr/bin/env bash

	files=(/tmp/clipmenu.3.$USER/*)

	newest=${files[0]}
	for f in "${files[@]}"; do
		if [[ $f -nt $newest ]]; then
  			newest=$f
		fi
	done

	if url=$(grep --only-matching --perl-regexp "http(s?):\/\/[^ \"\(\)\<\>\]]*" "$newest"); then
		xdg-open $url
	fi

NOTE: The script on top didn't work on Arch Linux but this one worked.

	#!/usr/bin/env bash

	files=($XDG_RUNTIME_DIR/clipmenu.5.$USER/*)

	newest=${files[0]}
	for f in "${files[@]}"; do
		if [[ $f -nt $newest ]]; then
			newest=$f
		fi
	done
	if url=$(grep --max-count=1 --only-matching --perl-regexp "http(s?):\/\/[^ \"\(\)\<\>\]]*" "$newest"); then
		xdg-open $url
	fi

3. You need to export your preferred browser.

`$ echo "export BROWSER='chromium'" >> .bashrc`

4. Adding a keybinding for a faster access.

I use DWM as a window manager so i need to add the keybinding to the config.h file.

`$ cd Suckless/dwm/`

`/Suckless/dwm $ vim config.h`

NOTE: For more info watch the video.
