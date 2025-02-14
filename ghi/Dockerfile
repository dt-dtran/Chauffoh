# Development Stage
FROM node:lts-bullseye as development

WORKDIR /app

COPY ./ghi/package.json ./ghi/package-lock.json ./

# Install all dependencies including dev dependencies
RUN npm install
COPY ./ghi ./

ENV NODE_ENV=development
ENV HOST=0.0.0.0
ENV PUBLIC_URL=http://localhost:3000
ENV REACT_APP_API_HOST=http://your-production-api-host:8000
ENV REACT_APP_USER_SERVICE_API_HOST=http://your-production-api-host:8000

# Production Stage
FROM node:lts-alpine as production
WORKDIR /app

COPY --from=development /app/package.json /app/package-lock.json ./
RUN npm ci --production
COPY ./ghi ./
RUN npm run build

FROM node:lts-alpine
WORKDIR /app

COPY --from=production /app/build ./build
# Expose the port that the application will run on
EXPOSE 3000

# Set environment variables for production
ENV NODE_ENV=production
ENV HOST=0.0.0.0
ENV PUBLIC_URL=https://rent-a-driver1.gitlab.io/module3-project-gamma
ENV REACT_APP_API_HOST=https://mar-9-pt-chauffohapi.mod3projects.com
ENV REACT_APP_USER_SERVICE_API_HOST=https://mar-9-pt-chauffohapi.mod3projects.com


# Run the application
CMD ["npm", "start"]
