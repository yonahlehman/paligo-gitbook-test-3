# Format test (delete after checking)

Please look at each case and tell me which ones show the image correctly and at a sensible size.

## A. Block image resized to 300 px (figure)

<figure><img src="assets/Image_1456.png" alt="" width="300"><figcaption></figcaption></figure>

## B. Block image, plain Markdown (natural size)

![](assets/Image_1456.png)

## C. Images inside a numbered list

1. Step with a resized figure

   <figure><img src="assets/Image_1456.png" alt="" width="300"><figcaption></figcaption></figure>
2. Step with a plain Markdown image

   ![](assets/Image_1456.png)
3. Step with a raw img tag, resized

   <img src="assets/Image_1456.png" alt="" width="300">

## D. Icon inside a sentence

Line-size icon: click the icon <img src="assets/Check_New.png" alt="" data-size="line"> to continue.

Plain Markdown icon: click the icon ![](assets/Check_New.png) to continue.

## E. Icons inside table cells

| Style | Result |
|---|---|
| img with data-size line | <img src="assets/Check_New.png" alt="" data-size="line"> |
| img with width 24 | <img src="assets/Check_New.png" alt="" width="24"> |
| plain Markdown image | ![](assets/Check_New.png) |
