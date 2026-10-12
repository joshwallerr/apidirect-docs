# Substack Category IDs

Category IDs and slugs for the `category` parameter on [Category Publications](/docs/substack-category-publications) and [Category Feed](/docs/substack-category-feed). Substack has 33 leaderboard categories; each has a top board and a paid board of up to 525 publications and a rising board of up to 250. The 210 subcategories below appear in publication data but have no leaderboards. Either the numeric ID or the slug works. Two site-wide boards take a name instead: `bestsellers` (New Bestsellers, a rising list) and `podcasts` (Podcast Bestsellers).

**[Download substack-categories.json](https://apidirect.io/static/substack-categories.json)**

## Using a category ID

### Example: top Technology publications

```bash
curl "https://apidirect.io/v1/substack/category/publications?category=technology" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Example: rising Finance publications by ID

```bash
curl "https://apidirect.io/v1/substack/category/publications?category=153&tier=rising" \
  -H "X-API-Key: YOUR_API_KEY"
```

## Categories

| Category | ID | Slug |
|----------|----:|------|
| Culture | `96` | `culture` |
| Technology | `4` | `technology` |
| Business | `62` | `business` |
| U.S. Politics | `76739` | `us-politics` |
| Finance | `153` | `finance` |
| Food & Drink | `13645` | `food` |
| Wine & Spirits | `77018` | `wine` |
| Sports | `94` | `sports` |
| Art & Illustration | `15417` | `art` |
| World Politics | `76740` | `world-politics` |
| Health Politics | `76741` | `health-politics` |
| Fashion & Beauty | `49715` | `fashionandbeauty` |
| News | `103` | `news` |
| Music | `11` | `music` |
| Faith & Spirituality | `223` | `faith` |
| Climate & Environment | `15414` | `climate` |
| Science | `134` | `science` |
| Literature | `339` | `literature` |
| Fiction | `284` | `fiction` |
| Design | `61` | `design` |
| Health & Wellness | `355` | `health` |
| Travel | `109` | `travel` |
| Parenting | `1796` | `parenting` |
| Philosophy | `114` | `philosophy` |
| Comics | `387` | `comics` |
| Crypto | `118` | `crypto` |
| International | `51282` | `international` |
| History | `18` | `history` |
| Humor | `49692` | `humor` |
| Education | `34` | `education` |
| Film & TV | `76782` | `film-and-tv` |
| Home & Garden | `76866` | `home-garden` |
| Games | `76863` | `games` |

## Subcategories

No leaderboards; listed for reference.

### Culture

| Subcategory | ID | Slug |
|-------------|----:|------|
| Traditions & Customs | `76786` | `traditions-customs` |
| Cultural Commentary | `76780` | `cultural-commentary` |
| Festivals & Holidays | `76781` | `cultural-events-festivals` |
| Pop Culture | `76783` | `pop-culture` |
| Social Issues | `76784` | `social-issues` |

### Technology

| Subcategory | ID | Slug |
|-------------|----:|------|
| Emerging Tech | `76966` | `emerging-technologies` |
| Gadgets | `76967` | `gadgets-devices` |
| Digital Media | `76968` | `internet-social-media` |
| Substack | `77143` | `substack-platform` |
| Cybersecurity | `76965` | `cybersecurity` |
| Artificial Intelligence | `76964` | `artificial-intelligence-robotics` |
| Programming | `76969` | `programming-development` |
| Software | `76970` | `software-apps` |

### Business

| Subcategory | ID | Slug |
|-------------|----:|------|
| Career Development | `76750` | `career-development` |
| Productivity | `76755` | `productivity` |
| Entrepreneurship | `76751` | `entrepreneurship` |
| Leadership | `76752` | `leadership` |
| Marketing | `76753` | `marketing` |

### U.S. Politics

| Subcategory | ID | Slug |
|-------------|----:|------|
| U.S. Elections & Campaigns | `77041` | `us-elections-campaigns` |
| Midterms 2026 | `77142` | `midterms-2026` |
| U.S. Government & Policy | `77042` | `us-government-policy` |
| U.S. Political Satire | `77043` | `us-political-satire` |

### Finance

| Subcategory | ID | Slug |
|-------------|----:|------|
| Real Estate | `76832` | `real-estate` |
| Retirement Planning | `76833` | `retirement-planning` |
| Taxes & Accounting | `76834` | `taxes-accounting` |
| Banking & Credit | `76828` | `banking-credit` |
| Insurance | `76829` | `insurance` |
| Investing | `76830` | `investing` |
| Personal Finance | `76831` | `personal-finance` |

### Food & Drink

| Subcategory | ID | Slug |
|-------------|----:|------|
| Wine & Spirits | `77018` | `wine` |
| Baking | `76836` | `baking` |
| Cocktails | `77016` | `cocktails` |
| Coffee | `77017` | `coffee` |
| Restaurants | `76842` | `restaurants-dining-out` |
| Cooking & Recipes | `76838` | `cooking-recipes` |
| Food Culture | `76839` | `food-culture` |
| Food Industry | `76840` | `food-industry` |

### Sports

| Subcategory | ID | Slug |
|-------------|----:|------|
| Running | `77039` | `running` |
| Motorsports | `77038` | `motorsports` |
| Yoga | `77040` | `yoga` |
| American Football | `76956` | `american-football` |
| Baseball | `76957` | `baseball` |
| Cricket | `77037` | `cricket` |
| Golf | `76960` | `golf` |
| Soccer | `76959` | `football-(soccer)` |
| Basketball | `76958` | `basketball` |
| Hockey | `76961` | `hockey` |
| Tennis | `76962` | `tennis` |

### Art & Illustration

| Subcategory | ID | Slug |
|-------------|----:|------|
| Art History | `76742` | `art-history-criticism` |
| Art Supplies & Techniques | `76743` | `art-supplies-techniques` |
| Digital Art | `76744` | `digital-art` |
| Painting & Drawing | `76746` | `painting-drawing` |
| Photography | `76747` | `photography` |
| Mixed Media | `76745` | `mixed-media` |
| Sculpture | `76748` | `sculpture` |

### Fashion & Beauty

| Subcategory | ID | Slug |
|-------------|----:|------|
| Fashion Industry | `76814` | `fashion-industry` |
| Clothing & Apparel | `76813` | `clothing-apparel` |
| Accessories | `76812` | `accessories` |
| Fashion Trends | `76815` | `fashion-trends` |
| Hairstyling | `76816` | `hairstyling` |
| Makeup & Skincare | `76817` | `makeup-skincare` |
| Personal Style | `76818` | `personal-style` |

### News

| Subcategory | ID | Slug |
|-------------|----:|------|
| Breaking News | `76907` | `breaking-news` |
| World News | `76913` | `world-news` |
| Human Interest Stories | `76908` | `human-interest-stories` |
| National News | `76911` | `national-news` |
| Opinion Pieces | `76912` | `opinion-commentary` |
| Investigative Journalism | `76909` | `investigative-journalism` |
| Local News | `76910` | `local-news` |

### Music

| Subcategory | ID | Slug |
|-------------|----:|------|
| Album Reviews | `76899` | `album-reviews-analysis` |
| Concerts | `76900` | `concerts-festivals` |
| Electronic & Dance | `77028` | `electronic-dance` |
| Classical & Opera | `77026` | `classical-opera` |
| Country | `77027` | `country` |
| Folk | `77029` | `folk` |
| Hip-Hop & Rap | `77030` | `hip-hop-rap` |
| Jazz | `77031` | `jazz` |
| K-Pop | `77032` | `kpop` |
| Pop | `77033` | `pop` |
| Rock & Alternative | `77034` | `rock-alternative` |
| Music History & Theory | `76903` | `music-history-theory` |
| Music Industry | `76904` | `music-industry` |
| Musical Instruments | `76902` | `instruments-gear` |
| Music Production | `76905` | `music-production-technology` |

### Faith & Spirituality

| Subcategory | ID | Slug |
|-------------|----:|------|
| Judaism | `76809` | `judaism` |
| Meditation & Mindfulness | `77015` | `meditation-mindfulness` |
| Christianity | `76806` | `christianity` |
| Islam | `76808` | `islam` |
| Buddhism | `76805` | `buddhism` |
| Atheism | `76804` | `atheism-agnosticism` |
| New Age & Alternative Beliefs | `76810` | `new-age-alternative-beliefs` |
| Hinduism | `76807` | `hinduism` |

### Climate & Environment

| Subcategory | ID | Slug |
|-------------|----:|------|
| Pollution & Waste Management | `76760` | `pollution-waste-management` |
| Climate Change | `76757` | `climate-change` |
| Renewable Energy | `76761` | `renewable-energy` |
| Sustainable Living | `76762` | `sustainable-living` |
| Wildlife | `76763` | `wildlife` |
| Environmental Policy | `76759` | `environmental-policy-advocacy` |
| Conservation | `76758` | `conservation` |

### Science

| Subcategory | ID | Slug |
|-------------|----:|------|
| Psychology & Neuroscience | `76953` | `psychology-neuroscience` |
| Astronomy | `76948` | `astronomy-space` |
| Life Sciences | `76949` | `biology-life-sciences` |
| Engineering | `76954` | `technology-engineering` |
| Physics & Chemistry | `76952` | `physics-chemistry` |
| Medicine | `76951` | `medicine-healthcare` |
| Earth Sciences | `76950` | `earth-sciences-geology` |

### Literature

| Subcategory | ID | Slug |
|-------------|----:|------|
| Poetry | `76897` | `poetry` |
| Book Recommendations | `77024` | `book-recommendations` |
| Writing Craft | `77025` | `writing-craft` |
| Author Interviews | `76890` | `author-interviews` |
| Classic Literature | `76892` | `classic-literature` |
| Literary Fiction | `76895` | `literary-fiction` |
| Nonfiction | `76896` | `nonfiction` |
| Book Clubs | `76891` | `book-clubs-reading-groups` |
| Theater | `76893` | `drama-theater` |
| Literary Criticism | `76894` | `literary-criticism-analysis` |

### Fiction

| Subcategory | ID | Slug |
|-------------|----:|------|
| Science Fiction | `76825` | `science-fiction` |
| Short Stories | `76826` | `short-stories` |
| Fantasy | `76820` | `fantasy` |
| Historical Fiction | `76821` | `historical-fiction` |
| Horror | `76822` | `horror` |
| Mystery & Thriller | `76823` | `mystery-thriller` |
| Romance | `76824` | `romance` |

### Design

| Subcategory | ID | Slug |
|-------------|----:|------|
| Architectural Design | `76788` | `architectural-design` |
| Industrial Design | `76790` | `industrial-design` |
| Interior Design | `76791` | `interior-design` |
| Typography | `76792` | `typography` |
| UX/UI Design | `76793` | `ux/ui-design` |
| Graphic Design | `76789` | `graphic-design` |
| Web Design | `76794` | `web-design` |

### Health & Wellness

| Subcategory | ID | Slug |
|-------------|----:|------|
| Fitness | `76845` | `fitness` |
| Medical News | `76846` | `medical-news` |
| Alternative Medicine | `76844` | `alternative-medicine` |
| Mental Health | `76847` | `mental-health` |
| Nutrition | `76848` | `nutrition` |
| Personal Growth | `76849` | `personal-growth` |
| Self-care | `76850` | `self-care` |

### Travel

| Subcategory | ID | Slug |
|-------------|----:|------|
| Travel Tips | `76978` | `travel-tips-advice` |
| Cultural & Historical Travel | `76974` | `cultural-historical-travel` |
| Adventure Travel | `76972` | `adventure-travel` |
| Budget Travel | `76973` | `budget-travel` |
| Destinations | `76975` | `destinations` |
| Luxury Travel | `76977` | `luxury-travel` |

### Parenting

| Subcategory | ID | Slug |
|-------------|----:|------|
| Infants & Toddlers | `76926` | `infants-toddlers` |
| Pregnancy & Birth | `76928` | `pregnancy-birth` |
| School-Aged Children | `76929` | `school-aged-children` |
| Education & Development | `76924` | `education-development` |
| Teenagers | `76930` | `teenagers` |
| Family Activities | `76925` | `family-activities` |
| Parenting Tips | `76927` | `parenting-tips-advice` |

### Philosophy

| Subcategory | ID | Slug |
|-------------|----:|------|
| Logic & Critical Thinking | `76935` | `logic-critical-thinking` |
| Political Philosophy | `76938` | `political-philosophy` |
| Metaphysics | `76936` | `metaphysics-epistemology` |
| Existentialism | `77035` | `existentialism` |
| Philosophy of Mind | `76937` | `philosophy-of-mind` |
| Stoicism | `77036` | `stoicism` |
| Aesthetics | `76932` | `aesthetics` |
| Eastern Philosophy | `76933` | `eastern-philosophy` |
| Ethics | `76934` | `ethics-morality` |

### Comics

| Subcategory | ID | Slug |
|-------------|----:|------|
| Superheroes | `76770` | `superheroes` |
| Comic Strips | `76766` | `comic-strips` |
| Graphic Novels | `76767` | `graphic-novels` |
| Independent Comics | `76768` | `independent-comics` |
| Manga | `76769` | `manga` |
| Webcomics | `76771` | `webcomics` |

### Crypto

| Subcategory | ID | Slug |
|-------------|----:|------|
| Blockchain Technology | `76773` | `blockchain-technology` |
| Crypto Investing | `76776` | `cryptocurrency-trading-investing` |
| Crypto Regulations | `76774` | `crypto-regulations` |
| Decentralized Finance (DeFi) | `76777` | `decentralized-finance-(defi)` |
| Crypto Mining | `76775` | `cryptocurrency-mining` |
| NFTs | `76778` | `nfts` |

### International

| Subcategory | ID | Slug |
|-------------|----:|------|
| Africa | `76882` | `africa` |
| Asia | `76883` | `asia` |
| Middle East | `76885` | `middle-east` |
| North America | `76886` | `north-america` |
| Oceania | `76887` | `oceania` |
| South America | `76888` | `south-america` |
| Europe | `76884` | `europe` |

### History

| Subcategory | ID | Slug |
|-------------|----:|------|
| Genealogy | `76980` | `genealogy` |
| Military History | `76857` | `military-history` |
| Cultural History | `76855` | `cultural-history` |
| Modern History | `76858` | `modern-history` |
| Historical Events | `76856` | `historical-events` |
| Ancient History | `76852` | `ancient-history` |
| Archaeology | `76853` | `archaeology` |
| Biographies | `76854` | `biographies-memoirs` |

### Humor

| Subcategory | ID | Slug |
|-------------|----:|------|
| Humorous Essays | `76876` | `humorous-essays` |
| Satire | `76879` | `satire` |
| Stand-up Comedy | `76880` | `stand-up-comedy` |
| Internet Memes | `76877` | `internet-memes` |
| Parody & Spoofs | `76878` | `parody-spoofs` |
| Funny Stories | `76875` | `funny-stories-anecdotes` |
| Comedy TV & Movies | `76874` | `comedy-tv-movies` |

### Education

| Subcategory | ID | Slug |
|-------------|----:|------|
| Teaching Strategies | `76802` | `teaching-strategies` |
| Homeschooling | `77013` | `homeschooling` |
| Language Learning | `77014` | `language-learning` |
| Educational Technology | `76797` | `educational-technology` |
| Higher Education | `76798` | `higher-education` |
| K-12 Education | `76799` | `k-12-education` |
| Online Learning | `76800` | `online-learning` |
| Educational Policy | `76796` | `educational-policy` |
| Special Education | `76801` | `special-education` |

### Film & TV

| Subcategory | ID | Slug |
|-------------|----:|------|
| Emmy Awards | `77052` | `emmy-awards` |

### Home & Garden

| Subcategory | ID | Slug |
|-------------|----:|------|
| DIY Projects | `76867` | `diy-projects` |
| Home Improvement | `76870` | `home-improvement` |
| Organization & Cleaning | `76871` | `organization-cleaning` |
| Home Decor | `76869` | `home-decor` |
| Gardening | `76868` | `gardening-landscaping` |

### Games

| Subcategory | ID | Slug |
|-------------|----:|------|
| Tabletop Games | `77022` | `tabletop-games` |
| Video Games | `76981` | `video-games` |
