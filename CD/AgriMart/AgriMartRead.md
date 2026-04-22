📱 File 1 — Live Demo Website (agromart-demo.html)
A fully interactive simulation of the complete app with 12 real demo products (tomatoes, basmati rice, carrots, Alphonso mangoes, ghee, etc.). You can:

Browse the shop with category filters and search
Add products to cart, change quantities
Go through checkout with Paytm payment simulation (enter any UPI ID and hit Pay)
See the order success screen with a generated Order ID
Use the Farmer Dashboard (add products, view listings)
See the Admin Dashboard with orders table
Try the Login/Register modal with role selection


📖 File 2 — Complete Dev Guide (agromart-dev-guide.html)
A dark-themed guide with sidebar navigation covering all 19 sections. Every single import is included. Highlights:

pom.xml — All 12 dependencies, including all 3 JWT jars (the most common mistake people make)
application.properties — Every credential placeholder with comments telling you exactly where to get each key (MySQL, JWT secret command, Paytm MID, AWS IAM, Gmail App Password)
Complete entities — User, Role, Product, Order, OrderItem, Payment with full import lists
Paytm integration — Full checksum generation, callback verification, Angular redirect flow
schema.sql + seed-data.sql — Run these 2 files and get 11 demo products + 4 test users instantly
Deployment — EC2 + Docker + Netlify steps with exact commands
Credentials checklist — Table showing where to get every secret key
