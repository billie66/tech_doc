(setq ring-bell-function 'ignore)

;; disable toolbar
(tool-bar-mode -1)

;; disable scrollbar
(toggle-scroll-bar -1)

;; disable splash screen
(custom-set-variables '(inhibit-startup-screen t))

;; current buffer name in title bar
(setq frame-title-format "%b")

;; start emacs server
;;(server-start)

;;(custom-set-faces
  ;; custom-set-faces was added by Custom.
  ;; If you edit it by hand, you could mess it up, so be careful.
  ;; Your init file should contain only one such instance.
  ;; If there is more than one, they won't work right.
  ;;'(default ((t (:inherit nil :stipple nil :background "black" :foreground "white" :inverse-video nil :box nil
  ;; :strike-through nil :overline nil :underline nil :slant normal :weight normal :height 79
  ;; :width normal :foundry "unknown" :family "DejaVu Sans Mono")))))

;;to set background color to black
;;(set-background-color "black")

(require 'color-theme)
(load-file "~/.emacs.d/twilight-emacs/color-theme-twilight.el")
G(color-theme-twilight)


(add-to-list 'load-path "/home/billie/.emacs.d/muse-latest/lisp")

(require 'muse-mode)     ; load authoring mode

(require 'muse-html)     ; load publishing styles I use
(require 'muse-latex)
(require 'muse-texinfo)
(require 'muse-docbook)
(require 'muse-project)  ; publish files in projects

;; claim a project
(setq muse-project-alist
      '(("website" ("~/billie-home/muse" :default "index")
         (:base "peter-xhtml" :path "/var/www")
           )))
(muse-derive-style "peter-xhtml" "xhtml"
                   :header "~/billie-home/header/header.html"
                   :footer "~/billie-home/header/footer.html"
                   ;;:style-sheet peter-style-sheet)
                   )
(find-file "~/billie-home/muse/index.muse" t)
 ;;fill does not work
 ;;(auto-fill-mode -1)

