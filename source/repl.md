---
title: repl
date: 2020-05-07
---
Example Python program repl.py


## Code

Python example

    (defvar python-shell-send-code-step-on-function nil
      "If non-nil, step sending a function to the python interpreter.")
    
    (defun python-shell-step-after-defun ()
      (forward-paragraph)
      ;; when at last paragraph, don't step to beginning of "next" paragraph
      (unless (equal (line-number-at-pos (point))
                     (progn (forward-paragraph) (line-number-at-pos (point))))
        (backward-paragraph)
        (forward-line 1)))
    
    (defun python-shell-send-paragraph-and-step ()
      "Send current paragraph of code and move point to the beginning of next paragraph."
      (interactive)
      (save-excursion
        (let* ((beg (progn (forward-paragraph)
                           (backward-paragraph)
                           (unless (equal (line-number-at-pos) 1) 
                             (forward-line)) (point)))
               (end (progn (forward-paragraph) 
                           (unless (equal (line-number-at-pos (point))
                                          (line-number-at-pos (point-max)))
                             (forward-line -1))
                           (end-of-line)
                           (point)))
               (num-lines (1+ (- (line-number-at-pos end)
                                 (line-number-at-pos beg)))))
          (python-shell-send-region beg end)
          (message (concat 
                    (format "Sent %d line%s "
                            num-lines
                            (if (equal num-lines 1) "" "s"))
                    (if (equal num-lines 1) 
                        (format "(line %d)" (line-number-at-pos end))
                      (format "(lines %d-%d)" 
                              (line-number-at-pos beg) 
                              (line-number-at-pos end)))
                    " to Python interpreter")
                   (line-number-at-pos beg)
                   (line-number-at-pos end))))
      (python-shell-step-after-defun))
    
    (defun python-current-defun ()
      "`python-info-current-defun' doesn't work when on a blank line, for some reason."
      (interactive)
      (save-excursion (forward-paragraph)
                      (backward-paragraph)
                      (forward-line)
                      (python-info-current-defun)))
    
    (defun python-shell-send-code-and-step ()
      (interactive)
      ;; xemacs doesn't have use-region-p
      (unless (python-shell-get-process)
        (run-python))
      (cond ((use-region-p)
             (let ((end (region-end))
                   (beg (region-beginning)))
               (python-shell-send-region beg end)
               (message "Sent region between lines %d and %d to python interpreter"
                        (line-number-at-pos beg)
                        (line-number-at-pos end))
               (goto-char end)))
            ;; send function if in a function, else send block and iterate
            ((python-current-defun)
             (progn
               (python-shell-send-defun)
               (message "Sent '%s' function to python interpreter"
                        (propertize (python-current-defun) 'face
                                    '(:foreground "#66D9EF")))
               (when python-shell-send-code-step-on-function
                 (python-nav-end-of-defun)
                 (forward-line -1)
                 (python-shell-step-after-defun))))
            (t
             (python-shell-send-paragraph-and-step))))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
