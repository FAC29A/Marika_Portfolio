# Week 1-3: Understanding the Fundamentals
Understanding the fundamental building blocks of web pages. Examples are based on the project, <a href=https://github.com/FAC29A/ecoecho> EcoEcho </a>


## 1. Structure a site using semantic HTML to aid accessibility
<img width="597" alt="Screenshot 2023-10-09 at 20 08 01" src="https://github.com/FAC29A/Marika_Portfolio/assets/126022615/b2e6339c-d358-491a-ac57-ec008a04e7e7">

This screenshot shows how I took care to use various semantic elements. The use of `<header>`, `<nav>`, `<main>`, `<section>`, and `<footer>` helped create a clear layout of the site's content.

- **Header and Navigation**: I utilized the `<header>` and `<nav>` elements for branding (logo) and primary navigation. The use of `aria-label` in the navigation further aids accessibility by providing context to screen readers about the purpose of the navigation menu.

- **Main Content and Sections**: I encapsulated the primary content within the `<main>` tag, ensuring that the most crucial content gets a prominent semantic placement. Within this, I used `<section>` elements to separate different content areas, such as "About Our Agency," "Meet The Team," "Testimonials," and "Contact Us." Each section starts with a descriptive heading, providing an outline of the page's content.

- **Footer**: I used the `<footer>` element to contain information not critical to the main content. It offers context for additional interactions like sound toggle and copyright notice.


## 2. Ensure a web page is readable for screen readers
To facilitate a screen reader-friendly experience on the web page, I focused on the following implementations:
  
- **Lighthouse Testing**: Using Lighthouse, I identified areas of improvement, especially concerning image and video sizing. After optimisation, the site achieved a 100% accessibility score.

- **Image Descriptions**: Each image is equipped with descriptive `alt` text, ensuring screen readers can convey the image's significance, like "Marika's portrait, Client Immersion Specialist."

- **Contact Form**: The form is designed with semantic HTML tags, `aria-label`, and `aria-required` attributes, making it comprehensible and user-friendly for those using screen readers.


## 3. Ensure our UI has sufficient colour contrast so that everyone can perceive it comfortably

<img width="417" alt="Screenshot 2023-10-09 at 20 59 12" src="https://github.com/FAC29A/Marika_Portfolio/assets/126022615/0dc459b4-0509-4e99-9e8a-1a905b677997">

- **Text Colors**: Used a contrast of black (`#000`) on light backgrounds (`#f9f9f9`) and white (`#fff`) on dark backgrounds (`#333`) for legibility.
  
- **Buttons**: Dark buttons (`#333`) with light text offer clear readability, even with hover effects (`#555`).
  
- **Modals**: Utilized a semi-transparent black (`rgba(0, 0, 0, 0.7)`) to differentiate modal content from the background.

All colour choices were regularly tested with [WebAIM's Contrast Checker](https://webaim.org/resources/contrastchecker/) to meet accessibility standards.


## 4. Use various tools to check that our website meets accessibility criteria
<img width="672" alt="Screenshot_2023-09-26_at_20 29 20" src="https://github.com/FAC29A/Marika_Portfolio/assets/126022615/37984e69-914c-45e6-bde7-5cec1d74c6df">

- **LiveServer**: Used for real-time visualisation and testing during development.
  
- **Lighthouse**: Chrome's built-in Lighthouse functionality to analyse and improve accessibility scores. 


## 5. Use CSS media queries to ensure our content is always presented effectively on screens of different sizes
<img width="435" alt="Screenshot 2023-10-09 at 21 13 07" src="https://github.com/FAC29A/Marika_Portfolio/assets/126022615/4b5ef7db-fc93-4da7-b18b-fa24a1d14555">

- **Started Big**: I first designed for computer screens, making sure everything looked great on a big canvas.

- **Thinking Mobile**: I used media queries to tweak the design for screens up to `768px`. I adjusted fonts, images, and layouts to make sure it looked just right on smaller screens.

- **In-Between**: As an intermediate step, media queries targeting widths between `769px` and `1250px` were incorporated. This ensures that tablets and smaller laptops, which sit between mobile and full desktop screens, provide a well-balanced view of the content.


## 6. Demonstrate a mobile-first approach to building a website
<img width="435" alt="Screenshot 2023-10-09 at 21 18 55" src="https://github.com/FAC29A/Marika_Portfolio/assets/126022615/258b17fa-69ea-4cba-8248-9e98ef5817d6">


## 7. Use CSS variables to apply repeated colours to HTML elements

## 8. Use CSS Flexbox to style children in a single-direction layout (ie a row or a column)

## 9. Use CSS Grid to style children in two-direction layout

## 10. Ensure our Git commit history tells a coherent story

## 11. Use the appropriate input types in HTML forms for gathering different types of information
