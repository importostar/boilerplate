---
title: image_puzzle_game_final
date: 2020-05-07
---
Example Python program image_puzzle_game_final.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* from PIL import ImageTk, Image
* from tkinter import filedialog
* from tkinter import messagebox
* from resizeimage import resizeimage
* import time
* import random

## Methods

* def main():
* def mouse_button_click_event(event):
* def mouse_button_release_event(event):
* def show_win_messege_box():
* def generate_current_state():
* def swap_imageId(selection_imageId):
* def swap_images(selection):  # selection = list
* def is_game_over():
* def crop_original_image(image_orig):
* def create_images_for_labels():
* def create_labels():
* def create_imageid_for_labels():
* def bind_labels():
* def place_labels_on_grid():
* def open_new_image():
* def assign_image_to_label():
* def shuffle_images():

## Code

Python tkinter example

    from tkinter import *
    from PIL import ImageTk, Image
    from tkinter import filedialog
    from tkinter import messagebox
    from resizeimage import resizeimage
    import time
    import random
    
    PUZZLE_IMAGE_SIZE = 600
    IMAGE_COUNT = 9
    IMAGE_STATE = [0, 1, 2, 3, 4, 5, 6, 7, 8]
    selection = []
    selection_imageId = []
    DEFAULT_DIR = "Images_Viewer/art/contemp1.jpg"
    
    MAIN_WINDOW_WIDTH = 750
    MAIN_WINDOW_HEIGHT = 790
    
    current_state = []
    shuffle_state = []
    
    images = []
    labels = []
    im_crops = []
    root = Tk()
    image_frame = LabelFrame(root, text="Open Image & Shuffle", padx=20, pady=20)
    
    
    def main():
        root.title('Picture Puzzle Game')
        # positioning the main window in the middle of a screen
        # ws = root.winfo_screenwidth()
        # hs = root.winfo_screenheight()
        # x = (ws / 2) - (MAIN_WINDOW_WIDTH / 2)
        # y = (hs / 2) - (MAIN_WINDOW_HEIGHT / 2)
        # root.geometry('%dx%d+%d+%d' % (MAIN_WINDOW_WIDTH, MAIN_WINDOW_HEIGHT, x, y))
        #
        # # root.geometry('750x790')
        # root.maxsize(width=MAIN_WINDOW_WIDTH, height=MAIN_WINDOW_HEIGHT)
        # root.minsize(width=MAIN_WINDOW_WIDTH, height=MAIN_WINDOW_HEIGHT)
    
        image_frame.pack(padx=20, pady=20)
        image_orig = Image.open(DEFAULT_DIR)
        crop_original_image(image_orig)
        create_images_for_labels()
        create_labels()
        create_imageid_for_labels()
        bind_labels()
        place_labels_on_grid()
    
        open_file_button = Button(root, text="Open Image", command=open_new_image)
        open_file_button.pack()
    
        shuffle_button = Button(root, text="Shuffle", command=shuffle_images)
        shuffle_button.pack()
    
        exit_button = Button(root, text="Exit", command=root.destroy)
        exit_button.pack()
    
        root.mainloop()
    
    
    # function to be called when mouse enters in a label
    def mouse_button_click_event(event):
        event.widget['relief'] = RAISED
    
    
    def mouse_button_release_event(event):
        event.widget['relief'] = RAISED
        selection.append(event.widget)  # <tkinter.Label object .!labelframe.!label3>
        selection_imageId.append(event.widget.imageId)
        if len(selection) == 2:
            generate_current_state()
            swap_images(selection)
            swap_imageId(selection_imageId)
            generate_current_state()
            if is_game_over():
                root.update()
                show_win_messege_box()
                print("Congratulation!")
    
    
    def show_win_messege_box():
        messagebox.showinfo(title='Winner message box', message="You mastered that puzzle!")
    
    
    def generate_current_state():
        current_state.clear()
        for i in range(IMAGE_COUNT):
            current_state.append(labels[i].imageId)
        return current_state
    
    def swap_imageId(selection_imageId):
        print('selection_imageId')
        print(selection_imageId)
        labels[current_state.index(selection_imageId[0])].imageId = selection_imageId[1]
        labels[current_state.index(selection_imageId[1])].imageId = selection_imageId[0]
        selection_imageId.clear()
    
    
    def swap_images(selection):  # selection = list
        print("ready to swap")
        tmp = selection[0]['image']  # pyimage1
        selection[0]['image'] = selection[1]['image']
        selection[1]['image'] = tmp
        selection[0]['relief'] = FLAT
        selection[1]['relief'] = FLAT
        selection.clear()
    
    
    def is_game_over():
        game_over = False
        if current_state == IMAGE_STATE:
            game_over = True
        return game_over
    
    
    def crop_original_image(image_orig):
        # cropping the original image into 9 pieces
        # global im_crops
        im_crops.clear()
        im_crop_1 = image_orig.copy()
        (left, upper, right, lower) = (0, 0, 200, 200)
        im_crop_1 = im_crop_1.crop((left, upper, right, lower))
        im_crops.append(im_crop_1)
    
        im_crop_2 = image_orig.copy()
        (left, upper, right, lower) = (201, 0, 400, 200)
        im_crop_2 = im_crop_2.crop((left, upper, right, lower))
        im_crops.append(im_crop_2)
    
        im_crop_3 = image_orig.copy()
        (left, upper, right, lower) = (401, 0, 600, 200)
        im_crop_3 = im_crop_3.crop((left, upper, right, lower))
        im_crops.append(im_crop_3)
    
        im_crop_4 = image_orig.copy()
        (left, upper, right, lower) = (0, 201, 200, 400)
        im_crop_4 = im_crop_4.crop((left, upper, right, lower))
        im_crops.append(im_crop_4)
    
        im_crop_5 = image_orig.copy()
        (left, upper, right, lower) = (201, 201, 400, 400)
        im_crop_5 = im_crop_5.crop((left, upper, right, lower))
        im_crops.append(im_crop_5)
    
        im_crop_6 = image_orig.copy()
        (left, upper, right, lower) = (401, 201, 600, 400)
        im_crop_6 = im_crop_6.crop((left, upper, right, lower))
        im_crops.append(im_crop_6)
    
        im_crop_7 = image_orig.copy()
        (left, upper, right, lower) = (0, 401, 200, 600)
        im_crop_7 = im_crop_7.crop((left, upper, right, lower))
        im_crops.append(im_crop_7)
    
        im_crop_8 = image_orig.copy()
        (left, upper, right, lower) = (201, 401, 400, 600)
        im_crop_8 = im_crop_8.crop((left, upper, right, lower))
        im_crops.append(im_crop_8)
    
        im_crop_9 = image_orig.copy()
        (left, upper, right, lower) = (401, 401, 600, 600)
        im_crop_9 = im_crop_9.crop((left, upper, right, lower))
        im_crops.append(im_crop_9)
    
    
    def create_images_for_labels():
        images.clear()
        # creating the images to assign to labels img_1 = ImageTk.PhotoImage(im_crop_1)
        for i in range(IMAGE_COUNT):
            images.append(ImageTk.PhotoImage(im_crops[i]))
    
    
    def create_labels():
        # creating the labels
        for i in range(IMAGE_COUNT):
            labels.append(Label(image_frame, image=images[i], text="label_" + str(i)))
    
    
    def create_imageid_for_labels():
        # Example: label_1.imageId = 1
        for i in range(IMAGE_COUNT):
            labels[i].imageId = IMAGE_STATE[i]
    
    
    def bind_labels():
        # Example
        # label_1.bind("<Button-1>", click)
        # label_1.bind("<ButtonRelease-1>", release)
        for i in range(IMAGE_COUNT):
            labels[i].bind("<Button-1>", mouse_button_click_event)
            labels[i].bind("<ButtonRelease-1>", mouse_button_release_event)
    
    
    def place_labels_on_grid():
        # placing labels in grid: label_1.grid(row=0, column=0)
        for x in range(IMAGE_COUNT // 3):
            for y in range(IMAGE_COUNT // 3):
                labels[x * 3 + y].grid(row=x, column=y)
    
    
    def open_new_image():
        root.filename = filedialog.askopenfilename(initialdir=DEFAULT_DIR, title="Select file",
                                                   filetypes=(("jpg files", "*.jpg"), ("all files", "*.*")))
        image_orig_open = Image.open(root.filename)
        image_width = image_orig_open.size[0]
        image_height = image_orig_open.size[1]
        if image_width > image_height:
            image_orig_open = resizeimage.resize_height(image_orig_open, PUZZLE_IMAGE_SIZE)
        else:
            image_orig_open = resizeimage.resize_width(image_orig_open, PUZZLE_IMAGE_SIZE)
    
        crop_original_image(image_orig_open)
        create_images_for_labels()
        assign_image_to_label()
        create_imageid_for_labels()
        bind_labels()
        place_labels_on_grid()
    
    
    def assign_image_to_label():
        for i in range(IMAGE_COUNT):
            labels[i]['image'] = images[i]
    
    
    def shuffle_images():
        shuffle_state = random.sample(IMAGE_STATE, len(IMAGE_STATE))
        print(shuffle_state)
        for i in range(IMAGE_COUNT):
            labels[i]['image'] = images[shuffle_state[i]]
            labels[i].imageId = shuffle_state[i]
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
