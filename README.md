# Family Chore Management App

A collaborative web application designed to help families manage household chores fairly and efficiently through a unique personal value system.

## Overview

The Family Chore Management App addresses common household challenges by allowing family members to:
- Create and schedule chores (one-time or recurring)
- Assign personal "dislike values" to tasks (1-10 scale)
- Pick chores on a first-come, first-served basis
- Earn value points based on how much others dislike the tasks they complete
- Track contributions and performance statistics

## Key Features

### 🏠 Family-Centered Design
- Single family unit per account
- Admin-managed family member addition
- Secure email/password authentication

### 📋 Smart Chore Management
- Create one-time or recurring chores (daily, weekly)
- Filter chores by status (Available, In Progress, Completed)
- First-come, first-served chore claiming system
- Self-verified completion process

### 💯 Personal Value System
- Each member assigns personal dislike values (1-10) to any chore
- Points earned = average of other family members' dislike values
- Encourages taking on tasks others find unpleasant
- Promotes fairness through objective contribution tracking

### 📊 Performance Tracking
- Individual statistics dashboard
- Total tasks completed counter
- Cumulative value points earned
- Recent family activity feed

## Technology Stack

- **Frontend**: React/Vue/Angular (TBD)
- **Backend**: Node.js/Python/Django/Ruby on Rails (TBD)
- **Database**: PostgreSQL/MySQL/MongoDB (TBD)
- **Platform**: Web application (desktop and mobile browsers)

## Development Status

🚧 **Current Phase**: Project Setup & Planning
- ✅ Product Requirements Document completed
- ✅ Implementation plan finalized
- 🔄 Technology stack selection in progress
- ⏳ Phase 1: Core User/Family Management (upcoming)

## Planned Development Phases

1. **Phase 1**: Project Setup & Core User/Family Management
2. **Phase 2**: Chore Definition & Basic Lifecycle
3. **Phase 3**: Personal Value System & Point Calculation
4. **Phase 4**: UI Views & Core Features Integration
5. **Phase 5**: Final Touches & MVP Polish

## User Roles

### Family Member
- Create, edit, and delete own chores
- Pick available chores to complete
- Assign personal values to any family chore
- Mark picked chores as completed
- View personal performance statistics

### Account Creator (Admin)
- All Family Member permissions
- Add new family members to the account
- Manage existing family member profiles
- Access family management section

## Data Architecture

### Core Entities
- **User**: Family member profiles and authentication
- **Family**: Family unit container and admin settings
- **Chore**: Task definitions with scheduling and status
- **UserChoreValue**: Personal dislike ratings (1-10 scale)
- **ChoreCompletion**: Completion records with calculated points

## Getting Started

### Prerequisites
- Node.js (version TBD)
- Database system (PostgreSQL/MySQL/MongoDB - TBD)
- Git

### Installation
```bash
# Clone the repository
git clone [repository-url]
cd family-chore-management-app

# Install dependencies (commands will vary based on chosen stack)
npm install  # or equivalent

# Set up environment variables
cp .env.example .env
# Edit .env with your database and other configuration

# Run database migrations
npm run migrate  # or equivalent

# Start development server
npm run dev  # or equivalent
```

## Contributing

This project follows a structured development approach with detailed implementation phases. Please refer to the implementation plan for specific development guidelines and testing requirements.

### Development Workflow
1. Each implementation step includes specific tasks and manual tests
2. All tests must pass before proceeding to the next step
3. Git commits are created after completing each step
4. Follow the established project structure and coding standards

## Future Enhancements

The current scope focuses on MVP functionality. Planned future features include:
- Advanced performance analytics and trends
- Configurable reward systems
- Push notifications for due dates
- Family leaderboards and achievements
- Calendar integration
- Photo verification for completion
- Mobile app versions

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For questions, issues, or feature requests, please open an issue in the GitHub repository.

---

**Note**: This application is currently in active development. Features and documentation will be updated as development progresses through the planned phases.