FROM node:18-slim AS build

WORKDIR /usr/src/app
COPY package.json package-lock.json ./

# Install Angular CLI and TypeScript globally
RUN npm install -g @angular/cli typescript

# Install dependencies and copy them to the container
RUN npm install
COPY . .

# Build the Angular application for production
RUN npm run build --prod

# Configure the nginx web server
FROM nginx:1.17.1-alpine
COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=build /usr/src/app/dist/client /usr/share/nginx/html

# Expose port 4000, which is what the node process is listening to
EXPOSE 4000

# Run the web service on container startup.
CMD ["nginx", "-g", "daemon off;"]
