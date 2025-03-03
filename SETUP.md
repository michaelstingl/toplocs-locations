# Local Development Setup Instructions

## Environment Setup

1. Create a `.env` file in the `locations-claude` directory with:
   ```
   VITE_SERVER_URL=http://localhost:3000
   VITE_MAPS_API_KEY=<google-maps-api-key>
   ```

2. This ensures the frontend communicates with your local backend server.

## Starting the Application

1. Start the tribelike-claude server first:
   ```
   cd ../tribelike-claude
   pnpm install
   pnpm run dev
   ```

2. Start the locations-claude frontend:
   ```
   cd ../locations-claude
   pnpm install
   pnpm run dev
   ```

3. The application is now available at http://localhost:5173 and communicates with the local backend at http://localhost:3000.

## Testing Registration Flow

1. On the login page, click "SignUp" to access the registration form
2. Fill in the required information
3. After successful registration, you should be redirected to the main application

## Troubleshooting

- If you encounter API errors, ensure both frontend and backend servers are running
- Verify your `.env` file has the correct URL for the backend server
- Check browser console for any JavaScript errors