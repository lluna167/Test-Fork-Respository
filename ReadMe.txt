Getting Started

Run the example REST service backend

CD todoRest && ../gradelew run

Run frontend in dev mode (requires 3 different terminals)

#listen on port 8888 and forwards the module path to gwt super dev mod and the everything else to webpak
cd todoMaterial && ../gradlew gwtDev

# runs webpack on port 8080 and also proxies requests to the rest service
cd todoMaterial && ../gradlew webpack5Dev

# becuase Vue GWT and SimpleRest use ASPT generation, run a continuous java build to trigger on changes
cd todoMaterial && ../gradelew compileJava --build-cache -t

Open browser to http://localhost:8888/

In dev mode a refresh will recompile GWT, CDD, JS, and webpack changes. 

Deploying

#deploy servie with proxy in front (/service/todo to localhost:12111)
cd todoRest && ../gradelew shadowJar
java -jar build/libs/todoRest-all.jar

#copy to archive in build/webapp to nginx or apache
cd todoMaterial && ../gradelew gwtArchive

Deploying using Docker

#make sure your user is in the cocker group or has permissions to docker service
docker build . -t todomaterial:latest
docker run -p 80:80 todomaterial

cd todoRest && ../gradelew dockerBuild
docker run -p 12111:12111 todoRest