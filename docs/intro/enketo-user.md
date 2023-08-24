---
title: Adopter Experience 👥
sidebar_label: Adopter Experience 📖
slug: /adopter-experience
---

<head>
  <title>Adopter Experience 👥</title>
  <meta name="description" />
</head>

## Introduction 📖
Hello and welcome, adopters! 🌟 <br/>
In this section, we will provide you with a comprehensive overview of the Adopter Experience for the  application. Whether you are a user, tester, or stakeholder, this documentation aims to familiarize you with the functionalities, features, and benefits of our application from an adopter's perspective.

### Table of Contents

- [User Journey Overview 🚀](#user-journey-overview)
- [Application Features and Usage 🌟](#application-features-and-usage)
- [Debugging and Troubleshooting 🐞](#debugging-and-troubleshooting)
- [Testing and Feedback 📊](#testing-and-feedback)
- [Providing Valuable Insights 🤝](#providing-valuable-insights)
- [Getting Help and Support 🆘](#getting-help-and-support)

## User Journey Overview 🚀

As an adopter of the application, your journey starts here. This section will guide you through the process of getting acquainted with the application and utilizing its features to meet your goals.

## Application Features and Usage 🌟

Our application offers a range of features designed to enhance your experience and productivity. From managing user interactions to accessing valuable insights, you'll find everything you need to achieve your objectives. Dive into our user-friendly interface, engage in meaningful conversations, and explore the power of intelligent automation.

### URLs Configuration and Environment Setup

The `urlsConfig` feature allows you to dynamically manage the URLs used by the application based on the environment you're operating in. This configuration is essential for connecting to various API endpoints and services. By following these steps, you'll be able to seamlessly switch between development and production environments without modifying the codebase:

1. **Accessing `urlsConfig`**:
   - In your application, you'll find a file named `urlsConfig.ts` or similar, where the URL configuration is defined.
   - Import the necessary types: `import { BaseUrls } from '@/types';`.

2. **Setting the Environment**:
   - The `environment` variable determines whether you're in a development or production environment. It's fetched from `process.env.NEXT_PUBLIC_ENVIRONMENT`.
   - If not specified, the default environment is 'development'.

3. **URLs Configuration**:
   - The `baseUrls` object contains URL configurations for both 'development' and 'production' environments.
   - Modify the values for `chatHistoryUrl`, `botDetailsUrl`, and `otpBaseUrl` to match your API endpoints.

4. **Accessing URLs Based on Environment**:
   - Use `urlsConfig` to access the correct URL for the current environment.
   - For example, to get the `chatHistoryUrl` for the current environment, use `urlsConfig.chatHistoryUrl`.

5. **Environment Console Logs**:
   - After setting up `urlsConfig`, you can log the chosen environment and the corresponding URLs using `console.log(environment)` and `console.log(urlsConfig)`.

6. **Switching Environments**:
   - When switching between development and production environments, update the `NEXT_PUBLIC_ENVIRONMENT` environment variable in your deployment settings.
   - The application will automatically use the correct URLs based on the environment.

By effectively utilizing the `urlsConfig`, you'll be able to effortlessly manage API endpoints and services across different environments. This ensures a seamless experience for both development and production scenarios, making your interactions with the application more efficient and reliable.

**Note:** It's important to ensure that your environment variables are correctly set up in your development and production environments for this feature to work as intended.

### Configuration Management with `config`

The `config` feature empowers you to centralize and manage various visual and functional aspects of your application in a single place. This includes settings for UI elements, icons, styles, URLs, and more. With the `config` object, you can effortlessly tailor your application's look and behavior without digging deep into the codebase. Let's dive into how to utilize and extend the `config` feature:

1. **Accessing `config`**:
   - Within your application, look for a file named `config.ts` or similar, where the application's configuration settings are defined.
   - Import any necessary assets or libraries based on your requirements.

2. **Configuration Structure**:
   - The `config` object is organized into different sections, such as `socket`, `list`, `starredlist`, `heading`, `tab`, `icon`, `search`, `chatList`, `chatItem`, `message`, and `chatWindow`.
   - Each section contains sub-settings to customize specific aspects of your application.

3. **Modifying Existing Settings**:
   - To adjust an existing setting, locate the appropriate section and change the desired properties.
   - For example, to change the text color of the chat icon, find the `icon` section and update the `colorScheme` property.

   <img src="https://i.postimg.cc/k4sjcB94/carbon-3.png" width="800px"/>

4. **Adding New Components**:
   - You can introduce new UI components to the `config` object.
   - Define a new section, such as `newComponent`, and configure its properties.
   - Access the new component in your code using `config.newComponent`.

5. **Importance of `config`**:
   - The `config` object centralizes your application's settings, promoting consistency and making it easier to manage changes.
   - It enhances collaboration, as developers can update settings without needing to touch other parts of the codebase.
   - This feature streamlines UI adjustments, making it efficient to fine-tune visual aspects across the application.

6. **Extending the `config`**:
   - As your application evolves, feel free to extend the `config` object with new sections and properties as needed.
   - This ensures that your application remains flexible and adapts to new requirements without major code modifications.

By harnessing the power of the `config` feature, you can quickly iterate on your application's appearance, behavior, and other settings. It encourages a modular approach to design and development, ultimately leading to a smoother and more maintainable codebase.

**Note:** While configuring the settings in `config`, be mindful of any dependencies or libraries used within your application to ensure seamless integration.

### Using ESLint, Prettier, and Husky for Code Consistency ✨

Maintaining consistent code quality and style is essential for collaborative development. We've integrated ESLint, Prettier, and Husky into our project to help you achieve code consistency effortlessly.

#### Setting Up ESLint and Prettier

1.**Installation**:
   - ESLint, Prettier, and other related packages are already listed in your `package.json` under `devDependencies`.
   - Run `npm install` to ensure all dependencies are installed.


2.**Configuration Files**:
   - ESLint: Configure ESLint rules in `.eslintrc.js`.
   - Prettier: Customize Prettier formatting options in `.prettierrc.js`.

3. **Running ESLint and Prettier**:
   - Use `npm run lint` to run ESLint and catch linting errors.
   - Use `npm run format` to apply Prettier formatting to `.ts`, `.tsx`, and `.md` files.

#### Running Lint and Format Scripts

We've set up two scripts to help you maintain code consistency:

1. **Linting** (`npm run lint`):
   - When you run `npm run lint`, ESLint will analyze your code for potential errors, style violations, and adherence to coding standards.
   - The main ESLint configuration file is located in the root of your project. It establishes global rules and settings.

2. **Formatting** (`npm run format`):
   - Running `npm run format` triggers Prettier to automatically format `.ts`, `.tsx`, and `.md` files according to the configuration in `.prettierrc.js`.
   - Prettier enforces a consistent code style, such as indentation, line breaks, and more.

#### ESLint Configuration for Different Directories

Our project follows a modular structure, and each directory might have specific coding standards. To accommodate this, we have individual ESLint configurations for each directory. These configurations can be found within the respective directories.

When you run `npm run lint`, ESLint will consider both the root configuration and any specific configurations in subdirectories. This ensures that your code adheres to the appropriate coding standards throughout the entire project.

For example:
- The root `.eslintrc.js` file contains global rules that apply to the entire project.
- In the `apps/uci` directory, you might find an `.eslintrc.js` file with rules tailored to the specific app.
- Similar `.eslintrc.js` files might be present in other directories, such as `packages/*` and `tsdx/*`.

#### Automating Code Consistency Checks with Husky

1. **Pre-Commit Hooks**:
   - Husky enables you to define actions that run automatically before commits are made.
   - Inside the `.husky` folder, you'll find a pre-commit hook file (e.g., `pre-commit`) that triggers linting and formatting checks before every commit.

2. **Customizing Pre-Commit Hooks**:
   - To add new pre-commit hooks, create additional executable files inside the `.husky` folder.
   - For example, create a file named `pre-commit-newhook` and add your desired actions, like running tests or additional linting tasks.

3. **Enforcing Consistency**:
   - When you attempt to make a commit, Husky will run the pre-commit hooks.
   - If any hook fails (e.g., ESLint finds issues or Prettier formatting is incorrect), the commit will be blocked, prompting you to fix the issues before proceeding.

#### Further Customization and Resources

1. **Adding More Hooks**:
   - Expand your `.husky` folder to include hooks for additional checks, like testing, security scans, or documentation validation.

2. **Learn More**:
   - Dive deeper into ESLint and Prettier configurations by referring to their official documentation:
     - ESLint: [Official Documentation](https://eslint.org/docs/user-guide/getting-started)
     - Prettier: [Official Documentation](https://prettier.io/docs/en/index.html)
   - Explore Husky's capabilities in its official documentation: [Official Documentation](https://typicode.github.io/husky/#/)

Now, you can focus on writing code while Husky and our consistent code tools take care of maintaining clean and formatted code automatically.

### Global Theme Management and Dark Mode 🎨

Maintaining a consistent and visually appealing user interface is crucial for any application. Our project provides a robust global theme management system that includes support for a dark mode. This allows you to seamlessly manage the appearance of your app and provide a better user experience.

### Theme Configuration

We've organized our theme configuration into a dedicated file, `theme.ts`, where you can customize various design elements to create a visually consistent app.

Here are some key components of the theme configuration:

- **`theme_styles`**: Contains a set of text styles, margins, paddings, and image dimensions. This helps maintain a consistent visual layout across the app.

- **`dark_theme`**: Defines the properties for the dark mode. It specifies background colors, font colors, and other visual elements that contribute to a cohesive dark mode experience.

- **`light_theme`**: Specifies the properties for the light mode, including background colors, font colors, and shadows.

<img src="https://i.postimg.cc/28SKgnXQ/carbon-1.png" />

#### Using the Theme Provider

We've implemented a `ThemeProvider` component that encapsulates the logic for theme management, including toggling between light and dark modes.

1. **Installation**:
   - To start using the theme provider, import it into your component file:

     ```javascript
     import { ThemeProvider, useTheme } from './ThemeProvider'; // Update the path as needed
     ```

2. **Implementation**:
   - Wrap your application's root component with the `ThemeProvider`:

     ```javascript
     function App() {
         return (
             <ThemeProvider>
                 {/* Your app's components */}
             </ThemeProvider>
         );
     }
     ```

3. **Using the Theme Context**:
   - To access the theme and toggle functionality, use the `useTheme` hook within your components:

     ```javascript
     import { useTheme } from './ThemeProvider'; // Update the path as needed

     function SomeComponent() {
         const { theme, toggleTheme } = useTheme();

         return (
             <div style={{ background: theme.background, color: theme.color }}>
                 {/* Your component's content */}
                 <button onClick={toggleTheme}>Toggle Theme</button>
             </div>
         );
     }
     ```

#### Customizing Theme Colors and Using Local Storage 🎨

Our global theme management system provides flexibility for adopters to customize the colors of the theme in both light and dark modes. Additionally, we utilize local storage to store and remember user preferences for the selected theme mode.

#### Customizing Theme Colors

To customize theme colors for both light and dark modes, follow these steps:

1. Open the `theme.ts` file in your project.

2. Locate the `dark_theme` and `light_theme` objects. These objects contain properties that define colors, backgrounds, and other visual elements for their respective modes.

3. Update the color values within the theme objects to your desired hex codes or color names. For example:

   ```javascript
   export const dark_theme = {
       // ...
       background: '#1E1E1E', // Update to your desired color
       color: '#FFFFFF',     // Update to your desired font color
       // ...
   };

   export const light_theme = {
       // ...
       background: '#FFFFFF', // Update to your desired color
       color: '#333333',     // Update to your desired font color
       // ...
   };


#### Importance of Theme Management

Consistent theming not only enhances the visual appeal of your app but also provides a seamless experience for users. Users can choose between light and dark modes based on their preference and lighting conditions.

By centralizing theme management, you simplify the process of maintaining a cohesive design language throughout your app. Whether you're building new components or expanding existing ones, you can confidently use the defined theme styles and elements to create a unified user interface.

Feel free to customize the theme properties in the `theme.ts` file to align with your app's branding and design guidelines.

Now you have the power to create a visually stunning and user-friendly app while ensuring that your design remains consistent across different screens and modes.


## Debugging and Troubleshooting 🐞

No software is immune to issues, and debugging is an essential part of the development process. This section provides guidance on how to effectively debug and troubleshoot potential problems in the application.

### 1. Browser Developer Tools

Modern browsers come with powerful developer tools that allow you to inspect, debug, and analyze your application. Here's how you can use them:

- **Console Logs**: Use `console.log()` statements in your code to print helpful information to the browser console. This can help you track the flow of your application and identify issues.

- **Network Tab**: Use the Network tab to monitor network requests and responses. This can help you identify incorrect API calls, response errors, or slow-loading resources.

- **Debugger**: Set breakpoints in your code using the Debugger tool. This allows you to pause the execution of your code and inspect variables, step through code, and analyze control flow.

### 2. Logging and Error Handling

Implement comprehensive logging and error handling in your application. When errors occur, make sure to catch and handle them gracefully. Logging error details can provide valuable insights into what went wrong:

- **Try-Catch**: Wrap sections of your code in try-catch blocks to handle exceptions and prevent application crashes. Log the error details using `console.error()`.

- **Error Boundary**: If you're using React, consider implementing Error Boundaries to catch and handle errors within components without crashing the whole application.

### 3. Remote Logging and Monitoring

Utilize remote logging and monitoring tools to gain visibility into your application's behavior in different environments:

- **Error Tracking Services**: Integrate error tracking services like Sentry or Rollbar to receive real-time alerts about errors occurring in your application.

- **Analytics Tools**: Implement analytics tools like Google Analytics to monitor user interactions and identify common user flow issues.

### 4. Debugging Redux State

Redux can sometimes introduce complex state management scenarios. Use these techniques to debug Redux-related issues:

- **Redux DevTools Extension**: Install the Redux DevTools browser extension. It provides an interactive interface to track state changes, dispatched actions, and more.

- **Time Travel Debugging**: Redux DevTools allows you to "time travel" through state changes, helping you understand how the state evolved to its current state.

### 5. Reproducing Issues

When debugging, it's crucial to be able to reproduce the issue consistently. Provide clear steps and context in bug reports to help others understand and fix the problem.

- **Steps to Reproduce**: Detail the exact steps that lead to the issue. Include information about the environment (browser, OS, etc.).

- **Code Snippets**: If applicable, include relevant code snippets in your bug reports to help others identify potential issues quickly.

## Testing and Feedback 📊

Your feedback is invaluable to us. As an adopter, you have the opportunity to test and explore new features before they are released to the wider audience. Your insights help us identify potential improvements and address any issues, ensuring a seamless experience for all users.

## Providing Valuable Insights 🤝

Your engagement with our application generates data that is analyzed to provide actionable insights. These insights empower you to make informed decisions and optimize your interactions. Discover trends, identify patterns, and leverage data-driven recommendations for improved outcomes.

## Getting Help and Support 🆘

At UCI, we prioritize your success. If you encounter any challenges or have questions, our dedicated support team is here to assist you. Whether you need technical guidance or assistance with using specific features, we're just a message away.

---

Embark on your journey with our application, and discover a world of possibilities. We're committed to delivering an outstanding experience that empowers you to achieve your goals, foster meaningful connections, and drive innovation.

**Author:** Tushar Banik <br/>
**Contact:** [Email](emailto:evilden982@gmail.com)
