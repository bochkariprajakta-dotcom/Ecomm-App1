# Stage 1 : Build Stage
FROM node:22-alpine AS builder

#  set the working directory in the application
WORKDIR /app

# copy package files
COPY package*.json ./
COPY prisma ./prisma/

#  install all the dependencies
RUN npm install

# generate prisma client
RUN npx prisma generate

# copy the rest
COPY . .

# building the application
RUN npm run build

# Stage 2 : Production Stage
FROM node:20-alpine AS production

WORKDIR /app

# copy package file
COPY package*.json ./

# install dependencies
RUN npm install --only:production

# copy the built from the builder stage
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/prisma ./prisma

# generate prisma client
RUN npx prisma generate

# expose port
EXPOSE 3001

# the command to run the dist
CMD ["node", "dist/app.js"]




# Node version-package we are using to build the application
FROM  AS builder

# Set up the work directory


# Copy the package files


# run the install command


# copy the entire code base


# run the build command


# something different  
FROM nginx:alpine AS production

COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
