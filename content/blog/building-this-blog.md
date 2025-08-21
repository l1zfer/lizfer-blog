+++
date = '2025-08-21T10:00:00+01:00'
draft = false
type = 'blog'
title = 'Building This Blog: A Journey from Hugo to AWS Amplify'
+++

Have you ever wanted to create a personal blog that's fast, secure, and easy to maintain? That's exactly what I set out to do with this blog. In this post, I'll walk you through my journey of building this blog using Hugo static site generator and hosting it on AWS Amplify. I'll share the technical decisions, challenges, and lessons learned along the way.

### A Journey Through Blogging Platforms (2002-2024)

Before diving into how I built this blog with Hugo, let me share my extensive journey through various blogging platforms. My blogging adventure started back in 2002, and I've experienced the evolution of blogging platforms firsthand:

1. **Early 2000s Brazilian Platforms** (2002-2005):
   - **Weblogger**: One of the first Brazilian blogging platforms
   - **Blogger.com.br**: The localized version of Blogger
   - **Blig**: A popular Brazilian blogging service
   These platforms were revolutionary for their time but had limited customization options and were dependent on their providers' availability.

2. **WordPress Era** (2005-2015):
   - Self-hosted WordPress installations
   - Dealing with PHP updates
   - Constant plugin maintenance
   - Database backups and migrations
   - Security patches and updates

3. **Medium** (2015-2023):
   - Clean writing interface
   - Built-in audience
   - Limited customization
   - Content ownership concerns
   - Platform dependency

### Why Hugo? A Modern Approach

After two decades of blogging experience, I chose Hugo for this blog for several compelling reasons:

1. **Content Ownership and Simplicity**:
   - Content is just Markdown files in a Git repository
   - No database to maintain or backup
   - Complete control over my content's format and structure
   - Easy version control and content history

2. **Layout Independence**:
   - Unlike WordPress or Medium, changing layouts doesn't require updating old posts
   - Theme changes are separate from content
   - Allows experimenting with different designs without touching the content

3. **Development Workflow**:
   - Write posts in my favorite text editor
   - Preview changes locally
   - Deploy through `git push`
   - Perfect integration with my daily development tools

4. **Performance and Security**:
   - Static files are incredibly fast to serve
   - No server-side code to exploit
   - No database to protect
   - No PHP or dynamic language vulnerabilities to worry about

5. **Cost and Maintenance**:
   - No database servers to maintain
   - Minimal hosting costs (just static files)
   - No plugin updates or compatibility issues
   - No security patches to apply

### The Beginning: Setting Up Hugo

Looking at the git history, this project started with a simple "Hello, World!" commit. Building on my previous blogging experience, I chose Hugo as my static site generator for several reasons:

1. **Speed**: Hugo is known for being one of the fastest static site generators
2. **Simplicity**: Markdown-based content creation
3. **Flexibility**: Extensive theming system and customization options
4. **Active Community**: Large ecosystem of themes and plugins

The initial setup was straightforward:

```bash
# Initial Hugo setup
hugo new site lizfer-blog
cd lizfer-blog
git init
```

### Hugo Configuration

Before diving into the theme, I set up the basic Hugo configuration in `hugo.toml`. Here are some key configurations:

```toml
baseURL = "https://lizfer.social"
title = "Luiz Ferreira - lizfer.social"
languageCode = "en-US"
enableRobotsTXT = true

[params]
  description = "Luiz Ferreira's personal blog about cloud architecture, DevOps practices, and tech career insights"
  favicon = "images/lizfer.png"
  images = ["images/lizfer.png"]
  title = "Luiz Ferreira - Cloud Solutions Architect"
```

I also configured the menu structure and social links:

```toml
[[menu.main]]
  identifier = "blog"
  name = "Blog"
  url = "/blog/"
  weight = 20

[[params.social]]
  name = "GitHub"
  icon = "github"
  url = "https://github.com/l1zfer"
```

For better code highlighting and markdown rendering, I added specific markup configurations:

```toml
[markup]
  [markup.highlight]
    style = 'friendly'
    lineNos = true
    lineNumbersInTable = false
    codeFences = true
```

### Theme Selection and Customization

The journey of finding the right theme was interesting. I went through a few iterations before settling on the current design. I started with a pre-built theme but eventually decided to customize it heavily to match my vision. The current theme is based on [Hugo Bear Blog](https://github.com/janraasch/hugo-bearblog), which I chose for its:

- Minimalist design
- Fast loading times
- Focus on content
- Dark mode support

### AWS Amplify Integration

One of the key decisions was hosting the blog on AWS Amplify. The commit `46c2944 Added changes to Amplify` marks this integration. The setup process was straightforward through the AWS Console, where I:

1. Created a new Amplify app
2. Connected it to my GitHub repository
3. Selected the main branch for production deployment
4. Configured the build settings for Hugo

The build settings in Amplify were configured to:
- Use the latest Hugo version
- Run `hugo build` command
- Deploy the contents of the `public` directory

AWS Amplify provides several benefits:

1. **Continuous Deployment**: Automatic builds and deployments from Git
2. **SSL/TLS**: Automatic HTTPS certificate management
3. **Global CDN**: Fast content delivery through CloudFront
4. **Branch Previews**: Easy testing of changes before production

The setup process involved:

1. Creating an Amplify app in the AWS Console
2. Connecting it to the GitHub repository
3. Configuring the build settings with a `amplify.yml` file
4. Setting up branch-based deployments

### Domain Setup

The final piece of the puzzle was setting up my custom domain `lizfer.social`. This involved several steps in AWS:

1. **Domain Registration in Route 53**:
   - Registered the domain through AWS Route 53
   - Automatically created a hosted zone with NS and SOA records
   - Cost was reasonable compared to other registrars

2. **Amplify Domain Configuration**:
   - Added the domain in Amplify Console
   - Amplify automatically requested an SSL certificate through ACM
   - Configured domain settings:
     ```
     Production branch (main): lizfer.social
     Subdomain settings: www.lizfer.social -> lizfer.social
     ```

3. **DNS Configuration**:
   - Amplify automatically added required CNAME records
   - Set up domain redirects (www to non-www)
   - Added custom DNS records for email verification

4. **SSL/TLS Setup**:
   - AWS Certificate Manager (ACM) handled SSL certificate
   - Automatic certificate renewal
   - Configured for both apex and www domains

### Design Philosophy and User Experience

The visual design of this blog was carefully crafted to reflect a business card aesthetic, with intentional choices for every element:

1. **Color Palette**:
   - Light mode background (`#F1E9D2`): A warm, pastel tone reminiscent of premium business cards
   - Dark mode background (`#2C2416`): A deep, rich tone that maintains the warmth while reducing eye strain
   - Text colors carefully chosen for optimal contrast:
     - Headings: `#222` (light) / `#eee` (dark)
     - Body text: `#444` (light) / `#ddd` (dark)
   - Links: `#3273dc` (light) / `#8cc2dd` (dark) for clear call-to-actions
   - Visited links: `#8b6fcb` for both modes, providing consistent navigation history

2. **Typography**:
   - Primary font: Fira Code (monospace)
     - Chosen for its excellent readability on both mobile and desktop
     - Monospace characteristics that enhance code snippets presentation
     - Consistent weight distribution that works well with our pastel color scheme
   - Line height of 1.6 for optimal readability
   - Responsive font scaling with a base size of 1em
   - Carefully crafted heading hierarchy for clear content structure

3. **Layout Decisions**:
   - Maximum content width of 720px for optimal line length
   - Centered header with circular profile image (100px x 100px)
   - Content-first approach with minimal distractions
   - Strategic padding (20px) and margins for comfortable reading
   - Blog post previews with clear visual hierarchy
   - Custom styles for code blocks and blockquotes that maintain readability

4. **Mobile-First Considerations**:
   - Responsive navigation with comfortable tap targets
   - Fluid typography that scales gracefully
   - Images optimized and responsive (`max-width: 100%`)
   - Smooth transitions and hover effects
   - Carefully structured blog post lists for mobile reading
   - Touch-friendly buttons and links with appropriate spacing

5. **Accessibility Considerations**:
   - Dark mode specifically designed for astigmatism
     - Instead of pure white text on black background (which can cause halation and visual stress)
     - Using softer colors: `#ddd` for text on `#2C2416` background
     - This reduces the "glow" effect that people with astigmatism often experience
   - High contrast ratios in both modes for better readability
   - Consistent spacing and layout to reduce eye strain
   - Carefully selected font weights that maintain clarity in both modes
   - Warm color palette that's easier on the eyes during long reading sessions

### The Final Touches

The last commit `e76ef60 Go-live final changes` included several optimizations:

1. SEO improvements
2. Social media meta tags
3. Performance optimizations
4. Content structure refinements

### Technical Stack Overview

Here's a complete overview of the technical stack:

- **Static Site Generator**: Hugo
- **Hosting**: AWS Amplify
- **Domain Management**: AWS Route 53
- **Version Control**: Git/GitHub
- **CSS Framework**: Custom CSS with minimal dependencies
- **Content**: Markdown files
- **Images**: Optimized and served through CloudFront CDN

### Lessons Learned

Throughout this journey, I learned several valuable lessons:

1. **Start Simple**: Begin with a basic theme and customize gradually
2. **Content First**: Focus on content structure before heavy customization
3. **Version Control is Key**: Git history helps track evolution and decisions
4. **Automation Matters**: AWS Amplify's automated pipeline saves time
5. **Performance Optimization**: Consider performance from day one

### Conclusion

Building this blog has been an exciting journey of learning and experimentation. The combination of Hugo and AWS Amplify provides a robust, scalable, and maintainable solution for a personal blog. The best part? It's all version controlled and automated, making future updates a breeze.

A huge shoutout to my colleagues [Tiago](https://tig.pt) and [André](https://vidicorner.com), for the inspiration.

If you're interested in building something similar, feel free to check out the [source code on GitHub](https://github.com/lizfer/lizfer-blog). I hope this post helps you in your own blogging journey!