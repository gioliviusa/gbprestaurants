# Analytics & Tracking Setup Guide for GBP Restaurants

## Overview
This guide walks you through setting up comprehensive analytics and conversion tracking for gbprestaurants.com to measure the impact of your SEO/GEO efforts.

---

## 1. Google Analytics 4 (GA4) Setup

### Step 1: Create GA4 Property
1. Go to [Google Analytics](https://analytics.google.com)
2. Click "Create" > "Property"
3. Enter property name: "GBP Restaurants"
4. Select "Web" as platform
5. Enter website URL: `https://gbprestaurants.com`
6. Click "Create"

### Step 2: Get Tracking ID
1. In Admin > Property Settings, copy your **Measurement ID** (G-XXXXXXXXXX)
2. Add this tracking code to ALL pages in `<head>`:

```html
<!-- Google Analytics 4 -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX', {
    'page_path': window.location.pathname,
    'page_title': document.title
  });
</script>
```

**Replace `G-XXXXXXXXXX` with your actual Measurement ID**

### Step 3: Verify Installation
1. In GA4, go to Admin > Data Streams
2. Click your property
3. Use Real-Time report to verify tracking is working
4. Visit your website and confirm events appear in real-time (within 1-2 seconds)

---

## 2. Google Search Console Setup

### Step 1: Verify Property
1. Go to [Google Search Console](https://search.google.com/search-console)
2. Click "Add Property"
3. Select "URL prefix" and enter: `https://gbprestaurants.com`
4. Choose verification method (easiest: HTML file or DNS record)
5. Complete verification

### Step 2: Submit Sitemap
1. In Search Console, go to Sitemaps (left menu)
2. Enter: `https://gbprestaurants.com/sitemap.xml`
3. Click "Submit"
4. Monitor indexing status in Search Console dashboard

### Step 3: Monitor Rankings
1. In Search Console, go to "Performance"
2. Set up filters for:
   - Queries containing: "restaurant" + your state names
   - Device type: Mobile
   - Country: United States
3. Track metrics weekly:
   - Total Impressions
   - Total Clicks
   - Average CTR
   - Average Position

---

## 3. Form Submission Tracking (Formspree Integration)

### Step 1: Verify Formspree Integration
Your form already submits to Formspree at: `https://formspree.io/f/mljbbedb`

### Step 2: Track in GA4
Add this JavaScript after your form submission:

```html
<script>
document.getElementById('contactForm').addEventListener('submit', function(e) {
  // Track form submission event
  gtag('event', 'form_submit', {
    'form_name': 'Restaurant Audit Request',
    'form_destination': 'Formspree',
    'event_category': 'engagement',
    'event_label': 'lead_capture'
  });
});
</script>
```

### Step 3: Set Up Goal in GA4
1. Go to Admin > Conversions
2. Click "New Conversion Event"
3. Create event: "form_submit"
4. Mark as conversion

---

## 4. Custom Event Tracking

### Track Location Page Visits
Add to each state page (e.g., california.html):

```html
<script>
gtag('event', 'page_view', {
  'page_title': 'California Service Page',
  'page_category': 'location_page',
  'location_state': 'California'
});
</script>
```

### Track Blog Post Views
Add to each blog post:

```html
<script>
gtag('event', 'page_view', {
  'page_title': 'How to Get More Google Business Profile Views & Calls',
  'page_category': 'blog_post',
  'blog_topic': 'GBP Optimization'
});
</script>
```

### Track Navigation Clicks
Add to navigation links:

```html
<script>
document.querySelectorAll('a[href*="/service/"]').forEach(link => {
  link.addEventListener('click', function() {
    gtag('event', 'location_page_click', {
      'link_text': this.textContent,
      'link_destination': this.href,
      'click_source': 'navigation'
    });
  });
});

document.querySelectorAll('a[href*="/blog/"]').forEach(link => {
  link.addEventListener('click', function() {
    gtag('event', 'blog_click', {
      'link_text': this.textContent,
      'link_destination': this.href,
      'click_source': 'navigation'
    });
  });
});
</script>
```

---

## 5. Key Metrics to Track Monthly

### Organic Search Performance
Track in Google Search Console:
- **Impressions**: How many times your site appears in search
- **Clicks**: How many people click through to your site
- **CTR**: Click-through rate (clicks ÷ impressions)
- **Average Position**: Where you rank on average

### Website Traffic (GA4)
- **Total Sessions**: Number of visitor sessions
- **New Users**: First-time visitors
- **Bounce Rate**: % of sessions that leave without action
- **Avg Session Duration**: How long visitors stay

### Local Ranking Metrics
- **Local Pack Rankings**: Track position for key restaurant keywords in each state
- **Google Business Profile Views**: Monitor monthly changes
- **Phone Calls/Direction Requests**: From GBP analytics

### Conversion Metrics
- **Form Submissions**: Track lead volume from each source
- **Location Page Visits**: Which state pages get most traffic
- **Blog Post Views**: Which content resonates
- **Call Tracking**: Phone calls from your GBP

---

## 6. Conversion Funnels (GA4 Setup)

### Create Funnel: Visitor → Contact Form
1. Admin > Explorations
2. Click "Create new" > "Funnel exploration"
3. Add steps:
   - Step 1: Initial session (source = organic search)
   - Step 2: Location page view (page contains "/service/")
   - Step 3: Form submission (event = form_submit)
4. Analyze where visitors drop off

### Create Funnel: Blog → Conversion
1. Click "Create new" > "Funnel exploration"
2. Add steps:
   - Step 1: Blog page view (page contains "/blog/")
   - Step 2: Location page view (page contains "/service/")
   - Step 3: Form submission (event = form_submit)
4. Identify which blogs drive most conversions

---

## 7. Monthly Reporting Framework

### Create GA4 Report
1. Admin > Custom Reports
2. Click "Create Report"
3. Add metrics:
   - Sessions
   - Users
   - Bounce Rate
   - Avg Session Duration
   - Conversions
4. Add dimensions:
   - Source/Medium (organic search vs. direct vs. referral)
   - Device Category (mobile vs. desktop)
   - Page (which pages get most traffic)

### Create Search Console Report
1. Download data monthly from Performance tab
2. Create spreadsheet tracking:
   - Total Impressions (month-over-month)
   - Total Clicks (month-over-month)
   - Average Position (track ranking improvement)
   - New keywords appearing in search

### Create Dashboard
1. Tools > Dashboard
2. Add cards:
   - Monthly organic sessions (line chart)
   - Form submissions by source (pie chart)
   - Location page traffic (bar chart)
   - Blog performance (table)

---

## 8. Expected Results Timeline

### Weeks 1-4
- ✓ Analytics tracking live
- ✓ Baseline metrics established
- ✓ First data collection complete

### Weeks 5-8
- +20-30% increase in organic impressions
- +10-15% increase in clicks to site
- 2-3 form submissions per month

### Months 2-3
- +50-80% increase in organic impressions
- +40-60% increase in clicks
- Local Pack appearances for key keywords
- 5-8 form submissions per month

### Months 3-6
- +100%+ increase in organic traffic
- +50-150% lead volume increase
- Established Local Pack ranking for 10+ keywords
- Consistent 15+ leads per month

---

## 9. Tools to Install

### Browser Extensions for Monitoring
1. **SEMrush SEO Toolbar**: Track rankings for keywords
2. **Moz Rank Tracker**: Monitor local search positions
3. **Google Search Console Status Check**: Quick GSC updates

### Rank Tracking Setup
1. Go to [SE Ranking](https://seranking.com) or [Semrush](https://semrush.com)
2. Add keywords you want to track:
   - "Google Business Profile management" + state
   - "Restaurant GBP services" + state
   - "Local SEO restaurants" + state
3. Track rankings daily
4. Create monthly reports showing position changes

---

## 10. Quick Setup Checklist

- [ ] GA4 installed on all pages (home, blog, states)
- [ ] Measurement ID verified in real-time
- [ ] Sitemap submitted to Search Console
- [ ] Property verified in Search Console
- [ ] Form submission tracking event created
- [ ] Location page events configured
- [ ] Blog post events configured
- [ ] Dashboard created for monthly review
- [ ] Conversion funnels set up
- [ ] Team members granted access to GA4 & GSC
- [ ] Monthly reporting process documented

---

## 11. Direct Links

**Google Analytics**: https://analytics.google.com
**Google Search Console**: https://search.google.com/search-console
**Google Business Profile**: https://www.google.com/business/
**Formspree**: https://formspree.io/f/mljbbedb

---

## Questions?

Need help setting up analytics? Contact: hello@gbprestaurants.com

For Formspree lead emails, check your Formspree dashboard at https://formspree.io
