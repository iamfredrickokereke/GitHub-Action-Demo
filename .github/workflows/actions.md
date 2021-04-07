name: CI/CD Pipeline for Azure webapp deployment
'on':
  push:
    branches:
      - master
  pull_request:
    types:
      - synchronize
      - closed
    branches:
      - master
jobs:
  build:
    if: >-
      github.event_name == 'push' || (github.event_name == 'pull_request' &&
      github.event.action != 'closed')
    runs-on: ubuntu-latest
    name: Building Job
    steps:
      - uses: actions/checkout@v2
      - run: |
          echo Job built successfully

           
  deploy:
    name: Deploying to Azure server
    runs-on: ubuntu-latest
    steps:
      - name: Setup Node x version
        uses: actions/setup-node@v1
        with:
          node-version: '10.x, 11.x, 12.x, 13.x, 14.x'
      - name: 'npm install, build, and test'
        run: |
          npm install
          npm run build --if-present
          npm run test --if-present
   


          
