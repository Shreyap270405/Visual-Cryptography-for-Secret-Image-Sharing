# Visual Cryptography - Final Deliverables & Documentation

This document contains supplementary material for your Computer Networks and Security (CNS) mini project presentation and evaluation.

---

## 1. Top 10 Viva Questions & Answers

**Q1: What is Visual Cryptography?**
**A1:** It is a cryptographic technique where visual information (images, text) is encrypted in such a way that the decryption can be performed entirely by the human visual system, without the aid of computers or mathematical calculations.

**Q2: Who introduced the concept of Visual Cryptography?**
**A2:** The concept was pioneered by Moni Naor and Adi Shamir in 1994 at the Eurocrypt conference.

**Q3: How does a 2-out-of-2 scheme work?**
**A3:** A secret image is divided into exactly two shares. Having one share reveals absolutely no information about the secret. You must have both shares (2 out of 2) to reconstruct and view the original image.

**Q4: Why does the reconstructed image look a bit blurry or grey?**
**A4:** This is caused by **pixel expansion**. Our algorithm turns 1 pixel into a 2x2 block (4 sub-pixels). A "white" area in the original image is represented by 2 white and 2 black sub-pixels when the shares are overlaid, meaning it loses 50% of its contrast and looks grey.

**Q5: Is it possible to crack the secret image if an attacker intercepts only Share 1?**
**A5:** No. The algorithm provides **unconditional security** (perfect secrecy). Because the pattern for Share 1 is chosen completely at random, it acts like a One-Time Pad. The key space is too large for brute force, and statistical analysis yields no patterns.

**Q6: Why must the input image be converted to black and white (binary) first?**
**A6:** Standard visual cryptography relies on the physics of light passing through transparent sheets (or being blocked by opaque ones). It cannot naturally process continuous gradients or colors, so the image must be thresholded into strict binary values first.

**Q7: What mathematical operation is used by the computer to simulate the physical stacking of shares?**
**A7:** A logical **Bitwise AND** operation. Assuming White is 1 (transparent) and Black is 0 (opaque), light only passes if both shares are transparent (`1 AND 1 = 1`).

**Q8: What is "Pixel Expansion" and why is it necessary?**
**A8:** Pixel expansion is the process of replacing one original pixel with a matrix of sub-pixels (e.g., 2x2). It is necessary because we need extra space to introduce the random noise (the 2 white and 2 black sub-pixels) required to hide the underlying secret.

**Q9: What happens if you try to combine two shares from different secret images?**
**A9:** The result will just be pure random noise (black and white static). Since the shares were not generated together with matching/inverted patterns, they will not align to form any recognizable shape.

**Q10: What is the main real-world application of Visual Cryptography?**
**A10:** It is highly useful in scenarios where computation devices cannot be trusted or are unavailable. Examples include secure voting systems, biometric verification (e.g., matching a fingerprint share against a database share), and sending secure bank PINs through the mail.

---

## 2. Demo Walkthrough (For Presentation)

*Use this script when demonstrating the project to your evaluator:*

1. **Start the Application:** Launch the desktop GUI or open the Flask web page.
2. **Explain the Goal:** "This project demonstrates secure image sharing. Our goal is to encrypt an image so securely that even if a hacker intercepts one piece, they get nothing."
3. **Upload the Secret:** Select a simple black-and-white image (e.g., a picture of a QR code or text saying "SECRET").
4. **Generate Shares:** Click 'Generate'. 
   - *Point to Share 1:* "Notice how Share 1 looks like pure TV static."
   - *Point to Share 2:* "Share 2 also looks like pure static. No patterns are visible."
5. **Reconstruct:** Click 'Reconstruct'. 
   - *Show the result:* "By simply overlaying the two shares, the original image magically appears. Notice that the computer didn't have to perform any complex decryption math—it just overlaid the pixels."
6. **Explain the Contrast:** "You'll notice the background is grey instead of white. This proves the algorithm worked! It's due to the 2x2 pixel expansion required to hide the data."

---

## 3. Test Cases

| Test Case ID | Test Scenario | Expected Result | Pass/Fail |
|---|---|---|---|
| **TC-01** | Upload a valid `.png` or `.jpg` image. | System accepts the image and displays it on the screen. | Pass |
| **TC-02** | Upload an invalid file format (e.g., `.pdf` or `.txt`). | System rejects the file and prompts the user for a valid image. | Pass |
| **TC-03** | Generate shares for the uploaded image. | System generates two distinct images (Share 1 and Share 2) that appear as completely random noise. | Pass |
| **TC-04** | Attempt to view original secret using only Share 1. | Share 1 reveals no discernible shapes, text, or outlines from the original image. | Pass |
| **TC-05** | Reconstruct the image by combining Share 1 and Share 2. | The original secret image is clearly visible, albeit with a 50% reduction in contrast. | Pass |

---

## 4. Sample Outputs

*In your physical report, you should insert actual screenshots here. Here is the text description of the expected visuals:*

- **Input Image:** A white background with the word "SECRET" written in bold black text. (Dimensions: 200x100).
- **Share 1 Output:** An image of dimensions 400x200. It looks entirely like random black and white static noise. No letters are visible.
- **Share 2 Output:** An image of dimensions 400x200. It also looks like random static noise. 
- **Reconstructed Output:** An image of dimensions 400x200. The word "SECRET" is clearly readable in black. The background, which was originally solid white, now appears as a checkerboard/grey pattern due to the combination of the random white and black sub-pixels.

---

## 5. Future Enhancements

If this project were to be expanded in the future, the following features could be added:

1. **Color Visual Cryptography:** Implementing advanced halftoning techniques to encrypt and decrypt full-color (RGB) images rather than just binary black-and-white images.
2. **k-out-of-n Secret Sharing:** Expanding the algorithm from a strict 2-out-of-2 scheme to a threshold scheme (e.g., 3-out-of-5), where any 3 shares out of 5 can reconstruct the image, but 2 shares reveal nothing.
3. **Steganography Integration:** Instead of generating shares that look like suspicious random noise, the algorithm could hide the shares inside ordinary, innocent-looking photographs (like pictures of cats or landscapes) to avoid drawing the attention of hackers.
4. **No-Pixel-Expansion Schemes:** Implementing advanced probabilistic algorithms that do not require expanding the image size by 4x, thereby saving bandwidth and storage space.
