# Domain Knowledge Library

This file contains domain-specific feature expectations, patterns, and quality standards for common application types. Agents should reference this when working on projects in these domains.

---

## Task Management Applications

### Baseline Features (MUST HAVE)
| Feature | Description | Why Essential |
|---------|-------------|---------------|
| Tasks CRUD | Create, read, update, delete tasks | Core functionality |
| Task Title + Description | Rich text descriptions | Users need to capture details |
| Due Dates | Date/time picker with timezone | Time management is core use case |
| Priority Levels | At least 3 levels (Low/Medium/High) | Helps users focus |
| Tags/Labels | Colored labels for categorization | Organization fundamental |
| Projects/Folders | Grouping mechanism | Scale beyond 10 tasks |
| Search | Full-text search across tasks | Find anything quickly |
| Filters | Filter by status, date, priority, tags | Focus on what matters |
| List View | Traditional task list display | Primary interaction mode |
| Subtasks | At least 1 level of nesting | Complex tasks need breakdown |
| Recurring Tasks | Daily/weekly/monthly/custom | Repeating work is common |
| Reminders | Notifications before due | Prevent missed deadlines |

### Expected Features (SHOULD HAVE)
| Feature | Description |
|---------|-------------|
| Calendar View | See tasks by date |
| Kanban Board | Visual workflow management |
| Assignees | Assign tasks to users |
| Comments | Discussion on tasks |
| File Attachments | Attach documents/images |
| Activity History | Track changes |
| Templates | Reusable task templates |
| Bulk Operations | Multi-select and edit |
| Keyboard Shortcuts | Power user efficiency |
| Dark Mode | Visual preference |

### Innovation Opportunities
- AI task prioritization
- Natural language task creation
- Smart scheduling suggestions
- Focus mode / time blocking
- Integration ecosystem
- Gamification elements

---

## Note-Taking Applications

### Baseline Features (MUST HAVE)
| Feature | Description | Why Essential |
|---------|-------------|---------------|
| Rich Text Editor | Bold, italic, headers, lists | Basic formatting needs |
| Folders/Notebooks | Organization hierarchy | Scale beyond 10 notes |
| Tags | Cross-cutting categorization | Notes span topics |
| Search | Full-text search | Find anything |
| Markdown Support | Standard syntax | Developer expectation |
| Links | Link between notes | Knowledge graphs |
| Export | PDF, Markdown, HTML | Portability |
| Import | From common formats | Migration path |
| Sync | Cross-device access | Modern expectation |
| Offline Mode | Work without internet | Reliability |

### Expected Features (SHOULD HAVE)
| Feature | Description |
|---------|-------------|
| Code Blocks | Syntax highlighting |
| Tables | Structured data |
| Images | Embed and paste |
| Templates | Quick start formats |
| Version History | Undo/recovery |
| Sharing | Collaborate on notes |
| Web Clipper | Save from browser |
| Backlinks | See what links to this note |

### Innovation Opportunities
- AI summarization
- Voice-to-note
- Smart linking suggestions
- Knowledge graph visualization
- Spaced repetition integration

---

## E-Commerce Applications

### Baseline Features (MUST HAVE)
| Feature | Description | Why Essential |
|---------|-------------|---------------|
| Product Catalog | Browse products | Core shopping experience |
| Product Details | Images, description, specs | Purchase decisions |
| Shopping Cart | Add/remove items | Purchase flow |
| Checkout | Payment collection | Revenue |
| User Accounts | Save preferences | Retention |
| Order History | Track purchases | Support/reorder |
| Search | Find products | Discovery |
| Categories | Browse by type | Navigation |
| Filters | Price, rating, etc. | Narrow options |
| Reviews/Ratings | Social proof | Trust |

### Expected Features (SHOULD HAVE)
| Feature | Description |
|---------|-------------|
| Wishlist | Save for later |
| Related Products | Cross-sell |
| Inventory Status | Availability |
| Multiple Payment Methods | Convenience |
| Guest Checkout | Reduce friction |
| Order Tracking | Shipping status |
| Discount Codes | Promotions |
| Mobile Responsive | Mobile shoppers |

### Innovation Opportunities
- AI recommendations
- Visual search
- AR try-on
- One-click reorder
- Subscription management

---

## Dashboard/Analytics Applications

### Baseline Features (MUST HAVE)
| Feature | Description | Why Essential |
|---------|-------------|---------------|
| Data Visualization | Charts, graphs | Make data understandable |
| Multiple Chart Types | Line, bar, pie, etc. | Different data needs |
| Filters | Date range, segments | Focus analysis |
| Responsive Layout | Any screen size | Access anywhere |
| Data Tables | Detailed data view | Drill down |
| Export | PDF, CSV, PNG | Share insights |
| Real-time Updates | Live data | Current information |
| Customizable Widgets | User preference | Personalization |

### Expected Features (SHOULD HAVE)
| Feature | Description |
|---------|-------------|
| Saved Views | Reusable configurations |
| Alerts/Thresholds | Automated monitoring |
| Comparison | Period over period |
| Drill-down | Explore details |
| Annotations | Mark events |
| Sharing | Team collaboration |
| Dark Mode | Long viewing sessions |

### Innovation Opportunities
- AI anomaly detection
- Natural language queries
- Predictive analytics
- Automated insights
- Embedded analytics

---

## Social/Community Applications

### Baseline Features (MUST HAVE)
| Feature | Description | Why Essential |
|---------|-------------|---------------|
| User Profiles | Identity | Personalization |
| Follow/Friend | Connections | Social graph |
| Feed | Content stream | Engagement |
| Posts/Content | Create content | User generated |
| Likes/Reactions | Engagement | Feedback loop |
| Comments | Discussion | Interaction |
| Notifications | Activity alerts | Retention |
| Search | Find users/content | Discovery |
| Privacy Controls | Who sees what | Trust |
| Reporting | Flag bad content | Safety |

### Expected Features (SHOULD HAVE)
| Feature | Description |
|---------|-------------|
| Direct Messages | Private communication |
| Groups/Communities | Shared interests |
| Hashtags | Topic discovery |
| Media Uploads | Images, video |
| Sharing | Spread content |
| Blocking | User safety |
| Bookmarks | Save content |

### Innovation Opportunities
- AI content moderation
- Interest-based recommendations
- Ephemeral content
- Live streaming
- Creator monetization

---

## API/Backend Services

### Baseline Features (MUST HAVE)
| Feature | Description | Why Essential |
|---------|-------------|---------------|
| RESTful Design | Standard patterns | Predictable |
| Authentication | JWT/OAuth | Security |
| Authorization | Role-based access | Permissions |
| Input Validation | Sanitize inputs | Security |
| Error Handling | Consistent responses | Debugging |
| Rate Limiting | Prevent abuse | Stability |
| Logging | Track operations | Debugging |
| Documentation | API reference | Usability |
| Versioning | Backward compatibility | Evolution |
| CORS | Cross-origin support | Web clients |

### Expected Features (SHOULD HAVE)
| Feature | Description |
|---------|-------------|
| Pagination | Large datasets |
| Filtering | Query flexibility |
| Sorting | Result ordering |
| Webhooks | Event notifications |
| Health Checks | Monitoring |
| Caching | Performance |
| Compression | Bandwidth |

### Innovation Opportunities
- GraphQL alternative
- Real-time subscriptions
- Auto-generated SDKs
- API analytics
- Smart caching

---

## How Agents Should Use This

### Dreamer
1. Identify the application type from user request
2. Check baseline features for that domain
3. Ensure ALL baseline features are in proposal
4. Look at innovation opportunities for differentiators

### Critic
1. Identify application type
2. Verify baseline feature coverage
3. Challenge missing baseline features
4. Evaluate innovations against opportunities list

### PM
1. Map baseline features to user stories
2. Prioritize: baseline = Must Have, expected = Should Have
3. Innovations = Could Have

### TechLead
1. Reference domain patterns for architecture
2. Consider domain-specific performance requirements
3. Apply domain security standards
