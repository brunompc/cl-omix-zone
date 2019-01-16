# cl-omix-zone

### HOT TO USE SKETCH LIB FROM LISP

https://github.com/vydd/sketch

1. Install MSYS2
    - http://repo.msys2.org/distrib/x86_64/msys2-x86_64-20180531.exe
    - Accept all default settings
    - Open msys2 shell and do updates / installs:
        - pacman -Syu' (like twice... follow instructions...)
        - pacman -Su
        - pacman -S git
        - pacman -S mingw-w64-x86_64-tk (for gui/gitk)
        - pacman -S mingw-w64-x86_64-emacs
        - pacman -S gcc libffi libffi-devel pkg-config
    - Add env var PATH 'C:\msys64\usr\bin'
    - Add env var GIT_GUI_LIB_DIR 'C:\msys64\usr\share\git-gui\lib' (from: https://github.com/valtron/llvm-stuff/wiki/Set-up-Windows-dev-environment-with-MSYS2)

2. Install SBCL
    - http://prdownloads.sourceforge.net/sbcl/sbcl-1.4.14-x86-64-windows-binary.msi
    - Accept all defaults settings with environment variables
    - Download DLLs from the following sites and put them in 'C:\Program Files\Steel Bank Common Lisp\1.4.14'
        - https://www.libsdl.org/release/SDL2-2.0.9-win32-x64.zip
        - https://www.libsdl.org/projects/SDL_image/release/SDL2_image-2.0.4-win32-x64.zip
        - https://www.libsdl.org/projects/SDL_ttf/release/SDL2_ttf-2.0.14-win32-x64.zip    [keep this 'zlib1.dll' file]
        - http://mirrors.ocf.berkeley.edu/gnu/emacs/windows/emacs-26/emacs-26.1-x86_64.zip    [get only the 'libffi-6.dll']

3. Restart computer (in order to apply env vars)

4. Emacs:
    - Add to .emacs
        - (require 'package)
        - (add-to-list 'package-archives '("melpa" . "http://melpa.milkbox.net/packages/"))
        - (package-initialize)
    - Eval previous expressions and do:
        - M-x package-refresh-contents
    - Install slime & company
        - M-x list-packages
        - search for *slime*, *company* and *slime-company* and press 'I' and in the end 'x' to install packages
        - note: depending on the emacs configuration this may change the .emacs
    - Add to .emacs
        - (setq inferior-lisp-program "C:/PROGRA\~1/STEELB\~1/1.4.14/sbcl.exe")
        - (setq slime-contribs '(slime-fancy))

5. Install quicklisp (inside emacs, do M-x slime)
    - Follow instructions from https://www.quicklisp.org/beta/ which is basically
        - (quicklisp-quickstart:install)
        - (ql:add-to-init-file)

6. Tests
    - Open a command window in win10
        - Start sbcl and do:
            (ql:quickload :swank)
    - In emacs do:
        - M-x slime-connect
        - In the new repl do:
            (ql:quickload :sketch)

0. (just ignore this part)
    - Building and installing libffi on Windows
        - https://proj.goldencode.com/projects/p2j/wiki/Building_and_Installing_libffi_on_Windows
