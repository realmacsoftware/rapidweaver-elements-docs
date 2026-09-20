---
description: Check your content, design, accessibility, SEO, privacy, performance, and publishing setup before launching a website
icon: rocket-launch
---

# Website launch checklist

Use this checklist before you publish a new website or make a major redesign live. Work through it in order, then repeat the final checks on the published site using a private browser window and a phone.

{% hint style="info" %}
Legal requirements vary by country, audience, and the data your website collects. Treat the privacy, terms, and cookie checks below as prompts rather than legal advice.
{% endhint %}

## Content and purpose

* [ ] **Make the purpose clear.** A first-time visitor should quickly understand who the website is for, what it offers, and what to do next.
* [ ] **Use one clear primary call to action.** Give each important page a clear next step, such as **Contact us**, **Book a consultation**, or **Buy now**.
* [ ] **Proofread every page.** Check spelling, grammar, dates, prices, opening hours, contact details, and claims.
* [ ] **Remove unfinished content.** Replace placeholder text and images, and hide pages that are not ready.
* [ ] **Check navigation.** Make sure page names are clear, the current page is easy to identify, and the logo returns visitors to the home page.
* [ ] **Add a useful footer.** Include relevant contact details and links to important legal pages.

## Privacy, terms, and consent

* [ ] **Publish a privacy policy.** Explain what personal data the site collects, why it is collected, who receives it, how long it is kept, and how visitors can contact you about it.
* [ ] **Publish terms and conditions when needed.** This is especially important when the site sells products or services, accepts bookings, creates accounts, or takes payments.
* [ ] **Configure cookie consent when required.** If the site uses non-essential cookies or tracking that requires consent, prevent those services from loading until the visitor has made a choice.
* [ ] **Check forms against the privacy policy.** Collect only the information you need and explain what will happen after someone submits it.
* [ ] **Make legal links easy to find.** Link the privacy policy, terms, cookie settings, and any returns or cancellation policy from the footer or another consistent location.

## Search and sharing

* [ ] **Set a unique browser title and meta description for every important page.** Keep them accurate, useful, and specific to the page.
* [ ] **Choose a social preview image.** Set the Open Graph image and check how the title, description, and image look when the page is shared.
* [ ] **Add a favicon and web icons.** Check them in browser tabs, bookmarks, and on mobile devices.
* [ ] **Use a logical heading structure.** Give each page one clear H1, followed by properly nested H2 and H3 headings.
* [ ] **Use readable page addresses.** Prefer short, descriptive URLs and avoid changing established URLs without redirects.
* [ ] **Check `sitemap.xml`.** Elements generates the sitemap automatically; confirm the live file includes the public pages you expect.
* [ ] **Review `robots.txt`.** Make sure it does not accidentally block the finished site or important pages from search engines.
* [ ] **Check the custom 404 page.** Explain that the page could not be found and provide links back to useful parts of the site.

See [SEO](seo.md), [Robots.txt](robots.txt.md), and [sitemap.xml](sitemap.xml.md) for setup details.

## Accessibility

* [ ] **Add useful alt text to meaningful images.** Leave alt text empty for images that are purely decorative.
* [ ] **Fix colour contrast problems.** Check text, buttons, links, form controls, and text placed over images in every colour mode.
* [ ] **Test with a keyboard.** Confirm that menus, links, buttons, forms, modals, and other controls can be reached and used without a mouse.
* [ ] **Make focus visible.** Keyboard users should always be able to see which control is selected.
* [ ] **Label forms clearly.** Use visible labels, helpful instructions, and understandable error messages.
* [ ] **Check link text.** Prefer descriptive wording over repeated phrases such as “click here”.
* [ ] **Review motion and media.** Avoid unexpected sound, provide captions or transcripts where appropriate, and respect reduced-motion preferences.

See [Accessibility](accessibility.md) for more detailed guidance and testing tools.

## Images and performance

* [ ] **Compress images before publishing.** Resize them to sensible dimensions and use an efficient format such as WebP where appropriate.
* [ ] **Remove unused large files.** Check Resources for obsolete images, videos, fonts, and downloads that unnecessarily increase the project or upload size.
* [ ] **Test page-loading speed.** Run important live pages through [PageSpeed Insights](https://pagespeed.web.dev/) or Lighthouse and investigate the largest problems.
* [ ] **Check fonts and third-party scripts.** Confirm they load correctly and remove services that add delay without enough benefit.
* [ ] **Look for layout movement.** Pages should not jump around as images, fonts, embeds, or cookie notices load.

## Responsive design

* [ ] **Check every important page at each Elements breakpoint.** Look for clipped text, horizontal scrolling, awkward gaps, overlapping content, and controls that are too small.
* [ ] **Test on real devices.** At minimum, use a current phone as well as the browser preview.
* [ ] **Check portrait and landscape layouts.** Navigation, forms, galleries, tables, and embedded media often need extra attention.
* [ ] **Zoom the page.** Important content and controls should remain usable when visitors enlarge the page or text.
* [ ] **Check dark mode if supported.** Confirm images, logos, text, controls, and contrast work in both appearances.

## Links, forms, and functionality

* [ ] **Fix broken links.** Test navigation, buttons, text links, downloads, email addresses, telephone links, social profiles, and external websites.
* [ ] **Test every form.** Submit valid and invalid entries, check required fields and error messages, and confirm the email or integration receives the submission.
* [ ] **Check success and failure states.** Visitors should understand whether an action worked and what they should do next.
* [ ] **Test interactive components.** Check menus, dropdowns, accordions, tabs, modals, sliders, filters, video, audio, and any custom components.
* [ ] **Complete a real customer journey.** Follow the path from the landing page to the main call to action without using the editor as a guide.

## Domain, security, and publishing

* [ ] **Confirm the publishing destination.** Check the server, folder, and site address before uploading.
* [ ] **Check the domain and DNS.** Test both the root domain and `www` version, and make one redirect consistently to the preferred address.
* [ ] **Enforce HTTPS.** Confirm all HTTP requests redirect to HTTPS and fix mixed-content warnings caused by insecure images, scripts, fonts, or embeds.
* [ ] **Back up the project.** Keep a restorable copy before the first launch or a major replacement.
* [ ] **Publish the complete site.** A full publish helps prevent old and new files from becoming mixed during the first launch.
* [ ] **Keep account details secure.** Store hosting, domain, analytics, and form credentials safely and make sure recovery information is current.

See [Publishing](../elements/publishing.md) for publishing setup and troubleshooting.

## Analytics and measurement

* [ ] **Install analytics if the site needs it.** Choose a service that fits the site's privacy requirements and your ability to act on the data.
* [ ] **Verify tracking on the live site.** Confirm page views and important events arrive in the correct account without counting preview traffic.
* [ ] **Respect consent choices.** Where consent is required, analytics and advertising tools must follow the visitor's selection.
* [ ] **Record the launch baseline.** Note the launch date and initial performance so future changes can be compared fairly.

See [Analytics](analytics.md) for instructions on adding site-wide or page-specific tracking code.

## Final live-site check

After publishing, open the public website in a private browser window and complete these checks again:

* [ ] Visit the home page through the final HTTPS domain.
* [ ] Check the main navigation, footer, and primary call to action.
* [ ] Submit each form and confirm delivery.
* [ ] Open several shared links and confirm their social previews.
* [ ] Visit a made-up address to test the 404 page.
* [ ] Check the site on a phone using mobile data as well as Wi-Fi.
* [ ] Confirm analytics, `sitemap.xml`, and `robots.txt` are live.
* [ ] Ask someone unfamiliar with the project to complete the site's main task and note anything that confuses them.

Once these checks pass, announce the site and keep monitoring forms, analytics, broken links, and performance during the first few days.
