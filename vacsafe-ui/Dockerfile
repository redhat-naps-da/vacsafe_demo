#  Build:  buildah bud -f vacsafe-ui/Dockerfile -t quay.io/redhat_naps_da/vacsafe-ui:0.0.5 vacsafe-ui
#  Push:   podman push quay.io/redhat_naps_da/vacsafe-ui:0.0.5
#  Run  :  podman run -it -p 8080:8080 --rm quay.io/redhat_naps_da/vacsafe-ui:0.0.5


# Stage 1: Compile and Build angular codebase

# Use official node image as the base image
FROM registry.access.redhat.com/ubi8/nodejs-14:1-43 as build

# Add the source code to app
COPY ./ .

# Install all the dependencies
RUN npm install

# Generate the build of the application (in: /opt/app-root/src )
RUN npm run build



# Stage 2: Serve app with nginx server

# Use official nginx image as the base image
FROM registry.access.redhat.com/ubi8/nginx-118:1-39

# Copy the build output to replace the default nginx contents.
COPY --from=build /opt/app-root/src/dist/ .

# Fix bug regarding refresh page with REACT apps
ADD nginx.conf "${NGINX_CONF_PATH}"

# Expose port
EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]

