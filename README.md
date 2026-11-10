# Love Running

Love Running is a static website for a running club based in Dublin, Ireland. It introduces the club, explains the benefits of running together, shares a weekly meet-up schedule, and lets visitors explore photographs and complete a sign-up form.

The site focuses on urban running around Dublin Docklands and trail running in Phoenix Park, with a social coffee meet-up included in the weekly schedule.

**Repository:** [ionuigbo10/love-running](https://github.com/ionuigbo10/love-running)

> The sign-up form sends data to an external demonstration endpoint. This repository does not contain a membership system, database, or server-side registration service. A live deployment URL has not been verified for this documentation.

## Contents

- [Project purpose](#project-purpose)
- [User goals](#user-goals)
- [Pages and features](#pages-and-features)
- [Design and layout](#design-and-layout)
- [Technology](#technology)
- [Project structure](#project-structure)
- [Run locally](#run-locally)
- [Sign-up form](#sign-up-form)
- [Accessibility and metadata](#accessibility-and-metadata)
- [Testing and validation](#testing-and-validation)
- [Known issues and limitations](#known-issues-and-limitations)
- [Deployment](#deployment)
- [Maintaining the site](#maintaining-the-site)
- [Credits and licensing](#credits-and-licensing)
- [Possible improvements](#possible-improvements)

## Project purpose

The website provides a central place for prospective runners to learn about the club and find information before attending a session. Its intended audience includes people looking for regular exercise, runners interested in road or trail sessions, and visitors seeking a social running community in Dublin.

## User goals

- Understand what the club offers and where it runs.
- Find the day, time, distance, and meeting point for a session.
- See photographs of running activities and events.
- Express an interest in joining and select a running preference.
- Move between the main pages using consistent navigation.

## Pages and features

### Home — `index.html`

The home page introduces the club with a full-width running photograph and a text overlay naming Dublin Docklands and Phoenix Park.

A benefits section presents four reasons to run with the club: **Feel Healthy**, **Feel Strong**, **Feel Free**, and **Get Social**. It includes icons and a circular running photograph.

The meet-up section displays the following schedule in cards over a Dublin city background. These details are the content currently stored in the HTML; they have not been independently confirmed as real events.

| Activity | Day | Distance | Meeting point | Time |
| --- | --- | --- | --- | --- |
| Urban | Monday | 5 km | The Marker Hotel | 18:30 |
| Trail | Wednesday | 10 km | The Phoenix Park | 18:30 |
| Urban | Friday | 5 km | The Marker Hotel | 18:30 |
| Trail | Saturday | 10 km | The Phoenix Park | 09:30 |
| Coffee | Sunday | 0 km | The Marker Hotel | 11:30 |

### Gallery — `gallery.html`

The gallery contains nine WebP photographs showing individual runners, group runs, races, and charity events. Every gallery image has an `alt` description. CSS columns arrange the photographs without a JavaScript gallery library.

The current stylesheet ultimately applies four columns at every viewport width because the last gallery column rule sits outside a media query. See [known issues](#known-issues-and-limitations) before describing the gallery as fully responsive.

### Sign Up — `signup.html`

The sign-up page places a form over a running photograph. Visitors can enter their first name, last name, and email address, then choose **Road**, **Trail**, or **Both** as their running preference. Road is selected by default.

The form uses native browser validation and a **Let's Run!** submit button. Submission behavior is described in [Sign-up form](#sign-up-form).

### Shared features

- A fixed header containing the linked Love Running logo.
- Home, Gallery, and Sign Up navigation links on every page.
- An underline identifying the current page.
- A checkbox-driven dropdown menu below the 768 px navigation breakpoint.
- A footer linking to Facebook, Twitter, YouTube, and Instagram.
- Social links that open in a new tab and include descriptive accessible labels and `rel="noopener"`.
- Favicons and shared search-engine metadata.

The social links currently point to the platforms' home pages, rather than club-specific profiles.

## Design and layout

### Typography and colour

Headings use **Oswald**, with uppercase text and letter spacing. Body text uses **Lato**. Both fonts are imported from Google Fonts, with sans-serif fallbacks.

| Use | Colour |
| --- | --- |
| Main text | `#3a3a3a` |
| Headings | `#252525` |
| Header background | `#ffffff` |
| Light text and borders | `#fafafa` |
| Hero overlay | `rgba(241, 109, 107, 0.7)` |
| Form overlay | `rgba(60, 60, 60, 0.6)` |
| Join button | `#454b1b` |
| Input hover accent | `#f16c6b` |

### Layout approach

The stylesheet uses Flexbox, CSS columns, background images, and media queries. The page body has a minimum viewport height and a flexible main area to help keep the footer below the content. Header offsets account for the fixed navigation.

Media queries appear at **576 px**, **768 px**, **992 px**, and **1200 px**. They contain gallery, navigation, hover, and benefits-layout adjustments. Some related rules currently fall outside their intended media-query blocks, so the presence of these breakpoints should not be treated as evidence that every mobile layout works correctly.

## Technology

| Technology or service | Role |
| --- | --- |
| HTML5 | Page structure, navigation, images, and form controls |
| CSS3 | Styling, layout, responsive rules, and menu visibility |
| Google Fonts | Lato and Oswald typefaces |
| Font Awesome | Navigation, benefits, activity, and social icons |
| WebP | Running photographs and background images |
| Code Institute form dump | External destination for demonstration form submissions |

There is no package manager configuration, build process, application framework, or custom JavaScript in this repository. Font Awesome is loaded through an external JavaScript kit.

## Project structure

```text
love-running/
├── index.html                 # Home, benefits, and meet-up schedule
├── gallery.html               # Nine-image running gallery
├── signup.html                # Sign-up form
├── README.md                  # Project documentation
└── assets/
    ├── css/
    │   └── styles.css         # Shared styles and media queries
    ├── favicon/               # Icons, manifest, and attribution
    │   ├── about.txt
    │   ├── site.webmanifest
    │   └── ...
    └── images/                # WebP photographs used across the site
```

## Run locally

### Open directly

Clone the repository, or download and extract a copy:

```bash
git clone https://github.com/ionuigbo10/love-running.git
cd love-running
```

Open `index.html` in a browser. The HTML and CSS do not require compilation or dependency installation.

### Use a local server

If Python 3 is installed, run this command from the project directory:

```bash
python3 -m http.server 8000
```

Visit [http://localhost:8000](http://localhost:8000). Stop the server with `Ctrl+C` in the terminal.

An internet connection is needed to load Google Fonts, the Font Awesome kit, and the external form destination. The local pages and image assets can be served without those services, but fonts, icons, and submission behavior may differ when they are unavailable.

## Sign-up form

The form uses `method="POST"` and submits to `https://formdump.codeinstitute.net`.

| Field label | Submitted name | Validation or default |
| --- | --- | --- |
| First Name | `first_name` | Required text |
| Last Name | `last_name` | Required text |
| Email Address | `email_address` | Required email input |
| Running preference | `running_preference` | Required radio group; `road` selected by default |

Preference values are `road`, `trail`, and `both`. Native browser validation checks required fields and basic email syntax before submission; it does not verify email ownership or create a club membership.

Submitted values are sent to the external endpoint. Use fictional details when testing. The repository contains no local data storage, custom success page, email notification workflow, or server-side validation implementation.

For an operational club website, replace the demonstration action with an appropriate registration service and document how submitted personal information is handled.

## Accessibility and metadata

The source includes:

- An English document language declaration.
- Semantic `header`, `nav`, `main`, and `footer` elements.
- Explicit labels associated with the sign-up inputs.
- Descriptive alternative text for gallery photographs.
- Accessible names on social links, including a new-tab notice.
- Viewport, description, and keyword metadata on every page.
- Apple touch and PNG favicon references.

These are implementation details, not a claim of accessibility conformance. The mobile navigation toggle needs particular attention: its checkbox is hidden with `display: none`, and its icon-only label has no explicit accessible name. The `.hidden-heading` utility also uses `display: none`, which removes those headings from the accessibility tree.

Keyboard behavior, focus visibility, contrast, zoom, and screen-reader output still require practical testing.

## Testing and validation

### Documentation review

This README was prepared by inspecting all three HTML pages, the shared stylesheet, favicon attribution, manifest, and repository configuration. That review identified the issues listed below. It did not include a browser compatibility assessment, validator run, accessibility audit, or live form submission.

No automated test suite is included in the repository. The following checklist is a repeatable manual test plan; its items are not recorded as passed.

| Area | Check | Expected result |
| --- | --- | --- |
| Navigation | Follow each menu link and the logo from every page | Correct destination opens; current page is underlined |
| Mobile menu | Toggle the menu below 768 px | Menu opens and closes without obscuring access to content |
| Keyboard | Navigate links, menu, form, and submit button using the keyboard | Controls are reachable and focus remains visible |
| Home | Inspect hero, benefits, and all five schedule cards | Text is readable and content is not clipped |
| Gallery | Inspect all nine images and resize the viewport | Images load, retain proportions, and remain useful at each width |
| Required fields | Attempt to submit an empty form | Browser blocks submission and identifies missing fields |
| Email | Enter an obviously malformed email address | Browser blocks submission |
| Preferences | Select Road, Trail, and Both in turn | Only one preference is selected at a time |
| Submission | Submit fictional values while online | Request reaches the external endpoint with the documented field names |
| Footer | Follow each social link | Intended platform opens in a new tab |
| External assets | Inspect fonts and icons with and without connectivity | Failures are understood and core content remains usable |
| Responsive layout | Inspect at 320, 375, 576, 768, 992, and 1200 px widths | No unwanted horizontal scrolling, clipping, or overlapping content |

For a fuller review, validate each HTML page and the stylesheet with W3C validators, inspect the browser console and network panel, and run an accessibility/performance audit. Record the browser versions, viewport sizes, findings, and fixes when those checks are completed.

## Known issues and limitations

1. **Gallery document declaration:** `gallery.html` starts with `!DOCTYPE html>` instead of `<!DOCTYPE html>`, which can cause quirks-mode rendering.
2. **Gallery column overrides:** Unconditional three-column and four-column rules follow the breakpoint rules. The final four-column declaration overrides the intended smaller-screen layouts.
3. **Sign-up positioning:** The form's absolute positioning and `top: 150px` apply globally. Absolute content does not contribute to its parent's normal-flow height, creating a risk of overlap or clipping, particularly on small screens.
4. **Benefits structure:** The benefits photograph is outside `#benefits` in the HTML. Flex ordering on `#benefits-image` therefore does not place it between the text groups inside that container.
5. **Mobile navigation accessibility:** The hidden checkbox and icon-only label need an accessible, keyboard-operable implementation.
6. **Hidden headings:** `display: none` hides headings from assistive technologies as well as visually.
7. **Demonstration integrations:** The sign-up endpoint is external, and footer links are generic platform links.
8. **External dependencies:** Font and icon availability depends on third-party services and the configured Font Awesome kit.
9. **Manifest setup:** `site.webmanifest` has empty application names and root-relative icon paths, and is not linked from the HTML pages. Its presence does not make this a configured installable web app.
10. **Unverified release status:** Browser testing, deployment, and performance results are not documented in the repository.

## Deployment

This is a static site. A compatible host only needs to serve the HTML files and the `assets` directory while preserving their relative paths. No build command or server-side runtime is required.

For GitHub Pages, configure the repository to publish from the branch containing the site and select the repository root as the publishing folder. Alternatively, upload the same files to another static host.

After publishing:

1. Record the actual deployment URL in this README.
2. Visit all three pages from that URL.
3. Check local images, styles, favicons, fonts, and icons.
4. Verify navigation and form behavior on desktop and mobile.
5. Confirm that any production registration destination and social profiles are appropriate.

The configured Git remote identifies the source repository; it does not confirm that GitHub Pages has been enabled or that a public deployment is available.

## Maintaining the site

- Edit meet-up days, distances, locations, and times in the `#times` section of `index.html`.
- Update gallery images and their alternative text in `gallery.html`.
- Change form fields or the submission destination in `signup.html`.
- Adjust shared typography, colours, backgrounds, and breakpoints in `assets/css/styles.css`.
- Update navigation, footer links, and shared metadata in all three HTML pages to keep them consistent.
- Keep asset paths relative and match filename capitalisation when adding or replacing files.
- Recheck affected pages at narrow and wide viewport widths after layout changes.

## Credits and licensing

### Fonts and icons

- **Google Fonts:** Lato and Oswald are imported by the shared stylesheet.
- **Font Awesome:** Icons are supplied by the kit referenced in all three HTML pages.
- **Code Institute:** The form action uses the Code Institute form dump endpoint. This establishes the form destination; it does not establish authorship of the rest of the project.

### Favicon attribution

The bundled [favicon attribution](assets/favicon/about.txt) identifies the running graphic as Twitter Twemoji artwork:

- Graphic: `1f3c3.svg`.
- Copyright: 2020 Twitter, Inc. and other contributors.
- Source: [Twitter Twemoji running graphic](https://github.com/twitter/twemoji/blob/master/assets/svg/1f3c3.svg).
- Licence: [Creative Commons Attribution 4.0](https://creativecommons.org/licenses/by/4.0/).

### Photographs and project licence

The photographs are stored in `assets/images/`. Their original sources and permissions are not recorded in the current repository; add verified credits and usage terms when available.

No project-wide licence file is currently included. Do not assume that the favicon licence applies to the source code, photographs, or other assets.

## Possible improvements

- Correct the HTML declaration and media-query placement.
- Make the sign-up layout fit its content at every viewport size.
- Improve mobile navigation semantics, keyboard support, and focus styles.
- Replace hidden headings with a visually hidden utility where appropriate.
- Add verified screenshots and completed testing results.
- Connect a production registration service and club-specific social profiles.
- Add verified photo credits and an explicit project licence.
- Consider lazy loading for gallery images after checking its effect on layout and performance.
