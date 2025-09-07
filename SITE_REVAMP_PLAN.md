# Carlos Sandoval - Personal Website Revamp Plan

## Overview
Transform the current academic-focused site into a comprehensive personal website showcasing professional work, personal projects, and lifestyle content including travel, diving, snowboarding, and jiujitsu.

## Current State Analysis
- Jekyll-based site with academic theme
- Currently has collections for: teaching, publications, portfolio, talks
- Location: Manila, Philippines
- Basic profile setup with GitHub integration

## New Site Structure

### 1. Homepage Redesign
- **Hero Section**: Personal introduction with rotating images from different life aspects
- **Quick Links**: Direct access to main content categories
- **Recent Posts**: Mixed feed of latest content from all categories
- **About Preview**: Brief personal statement covering professional and personal interests

### 2. Professional Section
#### Work Projects (`/work/`)
- **Current Role**: Highlight current position and responsibilities
- **Project Showcases**: Detailed case studies of significant work projects
- **Skills & Technologies**: Interactive skill matrix
- **Professional Timeline**: Career progression and achievements

#### Research & Publications (`/research/`)
- **Academic Publications**: Maintain existing IEEE publications
- **Research Projects**: Ongoing and completed research work

### 3. Personal Projects (`/projects/`)
- **Computer Science Projects**: 
  - Side projects and experiments
- **Technical Blog Posts**: Tutorials, learning notes, tech insights

### 4. Travel & Adventure (`/adventures/`)

#### Diving (`/adventures/diving/`)
- **Bohol**: Napaling Reef sardines (June 2024)
- **Bolinao**: Giant clams (July 2024)
- **Siquijor**: Sep 2024, Jan 2025, Mar 2025, May 2025
- **Anilao**: March 2025
- Photos and basic dive info for each location

#### Snowboarding (`/adventures/snowboarding/`)
- **Yuzawa**: Feb 2024, Mar 2024, Jan 2025
- **Nagano - Shiga Kogen**: Jan 2025
- Beginner to intermediate progression
- Equipment and resort info

#### Destinations (`/adventures/destinations/`)

**Southeast Asia**:
- **Bali**: July 2023, Dec 2023 - Ubud cafes, monkeys, Room4Desert
- **Bangkok**: Jan 2024, May 2024, June 2025 - Cafes, Muay Thai, work exhibitions
- **Hanoi**: Aug 2023 - Mountain tour with friends
- **Sagada**: April 2024 - Mountain trip

**Japan**:
- **Tokyo**: Feb 2024, Mar 2024 - Food, work exhibition
- **Osaka/Shimanami Kaido**: Nov 2024 - 5-day bike trip
- **Hokkaido**: Mar-Apr 2025 - Asahikawa, Furano, Niseko, Lake Toya, Noboribetsu, Jigokudani

**Other Countries**:
- **South Africa**: July 2023, Sep 2024 - Cape Town, near Kruger, BJJ training
- **Dubai**: Feb 2024, Feb 2025 - Work exhibitions
- **France**: Oct 2024 - SIAL Paris, La Rochelle
- **Italy/Spain**: May 2025 - Work trip Milano, Salamanca
- **USA**: Austin F1 GP, Vegas, Vancouver/Texas (May 2024) - BJJ training in Houston

### 5. Martial Arts (`/jiujitsu/`)
- **Training Journal**: Progress tracking and reflections

### 6. Blog (`/blog/`)
- **Book Reviews**: Reading list and thoughts

## Technical Implementation

### New Collections to Add
```yaml
collections:
  work:
    output: true
    permalink: /work/:path/
  adventures:
    output: true
    permalink: /adventures/:path/
  jiujitsu:
    output: true
    permalink: /jiujitsu/:path/
  projects:
    output: true
    permalink: /projects/:path/
```

### Navigation Structure
```yaml
navigation:
  - title: "About"
    url: /about/
  - title: "Work"
    url: /work/
  - title: "Projects"
    url: /projects/
  - title: "Adventures"
    url: /adventures/
    sublinks:
      - title: "Diving"
        url: /adventures/diving/
      - title: "Snowboarding"
        url: /adventures/snowboarding/
      - title: "Travel"
        url: /adventures/travel/
  - title: "Jiujitsu"
    url: /jiujitsu/
  - title: "Research"
    url: /research/
  - title: "Blog"
    url: /blog/
```

### Content Categories & Tags
- **Professional**: work, research, career, technology, programming
- **Adventure**: diving, snowboarding, travel, photography, exploration
- **Martial Arts**: jiujitsu, competition, training, philosophy
- **Personal**: life, reflection, books, photography, random
- **Technical**: coding, tutorials, tools, learning

## Content Strategy

### Phase 1: Foundation (Weeks 1-2)
1. **Site Structure Setup**
   - Create new collections and page templates
   - Update navigation and footer
   - Design responsive layouts for different content types

2. **Essential Pages**
   - Redesigned About page with personal story
   - Updated homepage with new layout
   - Contact page with multiple ways to connect

### Phase 2: Professional Content (Weeks 3-4)
1. **Work Portfolio**
   - Document 3-5 key professional projects
   - Create case studies with visuals and outcomes
   - Professional timeline and skills section

2. **Research Content**
   - Migrate existing publications
   - Add context and impact for each publication
   - Create research interests overview

### Phase 3: Personal Projects (Weeks 5-6)
1. **CS Projects**
   - Document top 5-8 personal coding projects
   - Create GitHub integration for recent work
   - Write technical blog posts about interesting projects

### Phase 4: Adventure Content (Weeks 7-10)
1. **Diving Content**
   - Create photo galleries from past dive trips
   - Write dive site reviews and experiences
   - Map-based dive log interface

2. **Snowboarding Content**
   - Season recap posts with photos and videos
   - Mountain and resort reviews
   - Gear recommendation posts

3. **Travel Stories**
   - Destination guides for places visited
   - Photo essays from different countries
   - Cultural experience stories

### Phase 5: Martial Arts & Blog (Weeks 11-12)
1. **Jiujitsu Section**
   - Training philosophy and journey
   - Competition experiences
   - Community and gym reviews

2. **Personal Blog**
   - Life reflection posts
   - Photography showcases
   - Book reviews and recommendations

## Visual Design Updates

### Photography Strategy
- **Hero Images**: Rotating collection showing different aspects of life
- **Adventure Galleries**: High-quality photos from diving, snowboarding, travel
- **Professional Headshots**: Updated professional photos
- **Action Shots**: Jiujitsu training and competition photos

### Layout Improvements
- **Card-based Design**: Modern card layouts for project showcases
- **Interactive Maps**: For dive sites and travel locations
- **Timeline Layouts**: For career progression and adventure chronology
- **Gallery Grids**: Optimized for photo-heavy content

### Brand Identity
- **Color Palette**: Ocean blues, mountain grays, martial arts reds
- **Typography**: Clean, readable fonts that work across content types
- **Logo/Avatar**: Personal logo incorporating elements from all interests

## SEO & Performance

### Content Optimization
- **Long-tail Keywords**: Target niche terms for diving, snowboarding, jiujitsu
- **Location-based SEO**: Philippines, diving spots, ski resorts
- **Technical Keywords**: Maintain CS and research-related SEO
- **Image Optimization**: Alt text, compression, responsive images

### Social Media Integration
- **Instagram**: Adventure photos and stories
- **LinkedIn**: Professional content and achievements
- **GitHub**: Code projects and contributions
- **YouTube**: Potential for adventure videos

## Maintenance & Growth

### Content Calendar
- **Monthly**: Adventure recap posts
- **Quarterly**: Professional project updates
- **Annually**: Year in review across all categories
- **Ongoing**: Technical blog posts and project documentation

### Analytics & Goals
- **Track Engagement**: Which content types perform best
- **Audience Growth**: Monitor visitor growth and retention
- **Content Goals**: Regular posting across all categories
- **Professional Impact**: Track how site affects career opportunities

## Success Metrics
1. **Diverse Content Library**: 50+ posts across all categories within first year
2. **Audience Engagement**: Comments and shares from different communities
3. **Professional Opportunities**: Contacts through the site
4. **Personal Documentation**: Comprehensive record of adventures and growth
5. **Community Building**: Connect with others in diving, snowboarding, jiujitsu communities

---

*This plan creates a holistic personal website that showcases Carlos as a multi-faceted individual - professional technologist, adventurous traveler, dedicated martial artist, and thoughtful human being.*