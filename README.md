```yml
name: CI/CD

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2

    - name: Set up Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '14'

    - name: Install dependencies
      run: npm install

    - name: Build the React app
      run: npm run build

    - name: Deploy to GitHub Pages
      env:
        ACTIONS_DEPLOY_KEY: ${{ secrets.ACTIONS_DEPLOY_KEY }}
      run: |
        npm install -g gh-pages
        gh-pages -d build -u "github-actions-bot <support+actions@github.com>" -r "https://${{ secrets.ACTIONS_DEPLOY_KEY }}@github.com/anonymous-leviathan/react-app-deployment-github-pages-via-github-actions.git"
```
```json
{
  "name": "my-app",
  "version": "0.1.0",
  "private": true,
  "homepage": "https://anonymous-leviathan.github.io/react-app-deployment-github-pages-via-github-actions",
  "dependencies": {
    "@testing-library/jest-dom": "^5.17.0",
    "@testing-library/react": "^13.4.0",
    "@testing-library/user-event": "^13.5.0",
    "@babel/plugin-proposal-private-property-in-object": "^7.21.11",
    "react": "^18.3.1",
    "react-dom": "^18.3.1",
    "react-scripts": "5.0.1",
    "web-vitals": "^2.1.4"
  },
  "scripts": {
    "deploy": "gh-pages -d build -u \"github-actions-bot <support+actions@github.com>\" -r https://anonymous-leviathan:${{ secrets.ACTIONS_DEPLOY_KEY }}@github.com/anonymous-leviathan/react-app-deployment-github-pages-via-github-actions.git",
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  "devDependencies": {
    "gh-pages": "^6.2.0"
  }
}
```
