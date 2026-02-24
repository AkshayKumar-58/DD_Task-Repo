# Building stage
FROM node:20-alpine AS build

#Creating Working directory
WORKDIR /app

#Copying package files first for better caching
COPY package*.json ./

#Install dependencies
RUN npm install

#Copy all remaining files
COPY . .

#Build the project
RUN npm run build

# Production stage
# Using lightweight Nginx image to serve static files
FROM nginx:1.25-alpine

#Copy built files from build stage into Nginx public folder
# /app/dist means default output folder for many frontend frameworks
COPY --from=build /app/dist /usr/share/nginx/html

#Expose port 80 (by default HTTP port)
EXPOSE 80

#Start Nginx in foreground mode
CMD ["nginx", "-g", "daemon off;"]