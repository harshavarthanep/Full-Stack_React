# Full-Stack_React
Use this to join your frontend and backend of full stack react project

1. First, rename the frontend to "client"
2. Move your backend to the root of frontend and name it "server"(it is already in that name)
3. Remove old node_modules from the frontend and backend
**4. server side:**
   on index.js rename to "server" add these lines
   
        const multer = require('multer');
        const path = require('path'); // Add this line
        const app = express();
  
          // Serve static files from the React app
        app.use(express.static(path.join(__dirname, '../client/build')));
        
        // Handle React routing, return all requests to React app
        app.get('*', (req, res) => {
          res.sendFile(path.join(__dirname, '../client/build', 'index.html'));
        });
        
        app.get('/', (req, res) => {
          res.send('Server is running');
        });
        
        
        //end of pro
        
        app.listen(port, () => {
          console.log(`Server is running on port ${port}`);
        });

**6. add package.json** 
  
       {
          "name": "server",
          "version": "1.0.0",
          "private": true,
          "scripts": {
            "start": "node serverlogin.js"
          },
          "dependencies": {
            "api": "^2.6.0",
            "bcrypt": "^5.1.1",
            "body-parser": "^1.20.2",
            "cors": "^2.8.5",
            "express": "^4.19.2",
            "express-session": "^1.18.0",
            "jsonwebtoken": "^9.0.2",
            "md5": "^2.3.0",
            "multer": "^1.4.5-lts.1",
            "mysql": "^2.18.1",
            "nodemailer": "^6.9.9"
          }
        }
   
**7. client side:**
   add package.json
   
         {
        "name": "client",
        "private": true,
        "version": "1.0.0",
        "scripts": {
          "dev": "vite",
          "build": "tsc && vite build",
          "preview": "vite preview",
          "start": "vite"
        },
       "dependencies": {
        "@ckeditor/ckeditor5-build-balloon": "^35.1.0",
        "@ckeditor/ckeditor5-build-balloon-block": "^35.1.0",
   
**8. in root(common for client and server)**
   add package.json
   
             {
          "name": "waveform-react",
          "version": "1.0.0",
          "private": true,
          "scripts": {
            "preinstall": "npm install --prefix client && npm install --prefix server",
            "start": "concurrently \"npm run server\" \"npm run client\"",
            "client": "npm start --prefix client",
            "server": "node server/serverlogin.js",
            "build": "npm run build --prefix client"
          },
          "dependencies": {
            "concurrently": "^7.0.0"
          }
        }

**9. it should look like**

  /my-app
  /client (React frontend)
    /src
    /public
    package.json (React-specific)
  /server (Node.js backend)
    serverlogin.js
  package.json (root)

Root Directory (e.g., Source - Login Page(SQL) - Full(OnProcess))
│
├── client
│   ├── public
│   ├── src
│   ├── package.json
│   └── ...
│
├── server
│   ├── serverlogin.js
│   ├── package.json
│   └── ...
│
├── package.json
└── ...


**10. now type the commands:**

    npm install (inside client directory)
    npm install (inside server directory)

From the root directory:

    npm install concurrently --save-dev
    npm run build --prefix client
    npm run install-client(optional)
    npm run install-server(optional)
    npm install(optional)
    npm start
    npm run build


**11. Ngix Optimization:**

    server {
      listen 80;
      server_name your_domain.com;
    
      root /var/www/your_app/client/build;
      index index.html;
    
      location / {
          try_files $uri /index.html;
      }
    
      location /api {
          proxy_pass http://localhost:3001;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection 'upgrade';
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
      }
    }



