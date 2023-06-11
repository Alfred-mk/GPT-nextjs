# [twitterbio.io](https://www.twitterbio.io/)

This project generates Twitter bios for you using AI.

[![Twitter Bio Generator](./public/screenshot.png)](https://www.twitterbio.io)

## How it works

This project uses the [ChatGPT API](https://openai.com/api/) and [Vercel Edge functions](https://vercel.com/features/edge-functions) with streaming. It constructs a prompt based on the form and user input, sends it to the chatGPT API via a Vercel Edge function, then streams the response back to the application.

If you'd like to see how I built this, check out the [video](https://youtu.be/JcE-1xzQTE0) or [blog post](https://vercel.com/blog/gpt-3-app-next-js-vercel-edge-functions).

## Running Locally

After cloning the repo, go to [OpenAI](https://beta.openai.com/account/api-keys) to make an account and put your API key in a file called `.env`.

Then, run the application in the command line and it will be available at `http://localhost:3000`.

```bash
npm run dev
```

## One-Click Deploy

Deploy the example using [Vercel](https://vercel.com?utm_source=github&utm_medium=readme&utm_campaign=vercel-examples):

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/Nutlope/twitterbio&env=OPENAI_API_KEY&project-name=twitter-bio-generator&repo-name=twitterbio)

## Notes
1. I would change the title of the web application

2. For the smartsheet.ts, I would use axios to connect to the smartsheet API endpoint
- I would have a function to create a new Smartsheet that has a try-catch block
- I would have a function to read Smartsheet details
- I would have a function to update a Smartsheet
- Finally I would have a function to delete a Smartsheet

3. Define example user schema for clients that may be interested in Precision services

interface User {
  id: string;
  firstName: string;
  lastName: string;
  email: string;
  phone: string;
  company: string;
  jobTitle: string;
  interests: string[];
  services: string[];
  address: Address;
}

interface Address {
  street: string;
  city: string;
  state: string;
  postalCode: string;
  country: string;
}

### get user ###
```bash
// Assuming you have an array of users called 'users'
function getUser(userId: string): User | undefined {
  return users.find(user => user.id === userId);
}
```
### get all users ###
```bash
/// Assuming you have an array of users called 'users'
function getAllUsers(): User[] {
  return users;
}
```
### get user property ###
```bash
// Assuming you have a user with id '34' and want to retrieve its 'property3'
function getUserProperty(userId: string, propertyKey: string): any | undefined {
  const user = getUser(userId);
  if (user) {
    return user[propertyKey];
  }
  return undefined;
}
```
### update user ###
```bash
// Assuming you have a user with id '34' and want to update it with new data
function updateUser(userId: string, updatedData: Partial<User>): boolean {
  const userIndex = users.findIndex(user => user.id === userId);
  if (userIndex !== -1) {
    users[userIndex] = { ...users[userIndex], ...updatedData };
    return true;
  }
  return false;
}
```

### update group of users ###
```bash
// Assuming you have an array of user IDs and want to update a specific property for each user
function updateGroupOfUsers(userIds: string[], updatedProperty: string, updatedValue: any): number {
  let updatedCount = 0;
  for (const userId of userIds) {
    const userIndex = users.findIndex(user => user.id === userId);
    if (userIndex !== -1) {
      users[userIndex][updatedProperty] = updatedValue;
      updatedCount++;
    }
  }
  return updatedCount;
}
```

### update all users ###
```bash
// Assuming you want to update a specific property for all users
function updateAllUsers(updatedProperty: string, updatedValue: any): void {
  for (const user of users) {
    user[updatedProperty] = updatedValue;
  }
}
```