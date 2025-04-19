# InsightPulse

InsightPulse is a flexible intelligence platform that transforms passive alerts into personalized, actionable insights for both individual and business users. It serves as a significant improvement over Google Alerts by not just notifying you of new content, but analyzing and contextualizing information to provide meaningful insights.

## Features

### For Individuals

- **Personal Interest Dashboard**: Track up to 20 topics with customizable alerts
- **Smart Prioritization**: Content is automatically prioritized based on relevance
- **Daily Briefings**: Receive customized summaries based on your priority settings
- **Smart Summarization**: Get concise information with the right level of detail
- **Learning System**: Improves relevance over time based on your interactions
- **Notification Preferences**: Choose when and how you receive updates

### For Businesses

- **Collaborative Workspace**: Team members can share and collaborate on insights
- **Custom Taxonomies**: Organize information according to your business structure
- **Integration Capabilities**: Connect with CRM, project management tools, and more
- **Pattern Recognition**: Identify trends and connections across multiple information sources
- **Scheduled Reports**: Generate reports on demand or on a schedule
- **Action Recommendations**: Get suggestions for how to respond to new information

## Technology Stack

InsightPulse is built using the following technologies:

- **Frontend**: Next.js 14 (App Router), React, TypeScript, Tailwind CSS
- **Authentication**: Supabase Auth with support for email/password, Google, Facebook, and LinkedIn
- **Database**: Supabase PostgreSQL for storing user data, alerts, and insights
- **Search**: Brave Search API for comprehensive web and news search
- **Autocomplete**: Floatype.js for search query autocomplete
- **Email Notifications**: Listmonk for managing subscriptions and sending emails
- **Payments**: Stripe for subscription management and recurring payments
- **AI Processing**: Integration with LLM providers for content analysis

## Getting Started

### Prerequisites

- Node.js 18+ and npm/yarn
- Supabase account (for database and authentication)
- Brave Search API key
- Stripe account (for payment processing)
- Listmonk setup (for email management)

### Installation

1. Clone the repository
   ```
   git clone https://github.com/yourusername/insightpulse.git
   cd insightpulse
   ```

2. Install dependencies
   ```
   npm install
   ```

3. Set up environment variables
   Copy the `.env.example` file to `.env.local` and fill in your API keys and configuration values.

4. Set up the database
   Run the SQL scripts in the `database` folder to set up your Supabase database schema.

5. Run the development server
   ```
   npm run dev
   ```

6. Open [http://localhost:3000](http://localhost:3000) in your browser

### Environment Variables

The following environment variables are required:

- `NEXT_PUBLIC_SUPABASE_URL`: Your Supabase project URL
- `NEXT_PUBLIC_SUPABASE_ANON_KEY`: Your Supabase anonymous key
- `NEXT_PUBLIC_BRAVE_SEARCH_API_KEY`: Your Brave Search API key
- `NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY`: Your Stripe publishable key
- `STRIPE_SECRET_KEY`: Your Stripe secret key
- `STRIPE_WEBHOOK_SECRET`: Your Stripe webhook secret
- `LISTMONK_API_URL`: Your Listmonk API URL
- `LISTMONK_API_KEY`: Your Listmonk API key

See `.env.local` for additional optional variables.

## Database Schema

InsightPulse uses the following main database tables:

- `users`: User accounts and profile information
- `subscriptions`: User subscription status and plan information
- `alerts`: Alert configurations created by users
- `insights`: Content and analysis derived from alerts

## API Routes

- `/api/search` - Search for content using Brave Search API
- `/api/alerts` - CRUD operations for managing alerts
- `/api/insights` - Fetch and manage insights
- `/api/subscriptions` - Manage user subscriptions
- `/api/process` - Process alerts and generate new insights

## Development

### Project Structure

```
/src
  /app                  # Next.js App Router structure
    /api                # API routes
    /dashboard          # Dashboard pages
    /signup             # Authentication pages
    /pricing            # Subscription plan pages
    ...
  /components           # Reusable React components
  /lib                  # Utility functions and services
    /contexts           # React contexts
    /hooks              # Custom React hooks
    /services           # Service modules for API integrations
    /supabase           # Supabase client and utilities
  /styles               # Global styles
```

### Testing

Run the test suite with:

```
npm run test
```

## Deployment

This application can be deployed to Vercel with the following command:

```
vercel
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgements

- The Brave Search team for their powerful search API
- Supabase for database and authentication services
- Vercel for hosting and deployment platform