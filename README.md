
## **Interactive Knowledge Map**

### **Project Description**  
This project displays an **interactive knowledge map** of courses and subjects. The map visually represents nodes (topics) and their relationships (links). Hovering over a node highlights the selected node and its connections, making it easier to understand the relationships.

---

### **Features**  
1. **Dynamic Hover Interaction**:  
   - Hovering over a node highlights it and its connected nodes and links.  
   - Unrelated nodes and links become slightly dimmed.  

2. **Interactive Visualization**:  
   - Nodes and connections are displayed in a clean, user-friendly graph format.  

3. **Customizable**:  
   - The colors, sizes, and transitions can easily be modified.  

---

### **Project Structure**  

```bash
project-root/
│── src/
│   │── components/
│   │   └── KnowledgeMap.vue     # The main knowledge map component
│   │── App.vue                  # The root app component
│   │── main.js                  # Vue entry point
│── public/
│   └── index.html               # Basic HTML template
│── package.json                 # Project dependencies
│── README.md                    # Instructions for installation and running
```

---

### **Prerequisites**  
Before running the project, make sure you have the following installed on your Linux system:

1. **Node.js** (version 14 or higher) and **npm**:  
   - Install via terminal:  
     ```bash
     sudo apt update
     sudo apt install nodejs npm
     ```

2. **Vue CLI**:  
   - Install globally using npm:  
     ```bash
     npm install -g @vue/cli
     ```

---

### **How to Install and Run the Project**  

1. **Clone the Repository**  
   Open your terminal and clone the project repository:  
   ```bash
   git clone <your-repository-url>
   cd <your-project-folder>
   ```

2. **Install Dependencies**  
   Use npm to install all the required packages:  
   ```bash
   npm install
   ```

3. **Run the Project**  
   Start the development server:  
   ```bash
   npm run serve
   ```

4. **Open the Application**  
   Once the server is running, open your browser and visit:  
   ```bash
   http://localhost:8080
   ```

---

### **Project Output**  

1. **Default View**:  
   - All nodes and connections are visible.  

2. **Hover Interaction**:  
   - Hovering over a node will:  
     - Highlight the node (blue color).  
     - Highlight connected nodes (green color).  
     - Highlight connections (orange lines).  
     - Dim all unrelated nodes and links.  

3. **Smooth Transitions**:  
   - The visual updates are smooth and responsive.  

---

4. ScreenShot:
   ![image](https://github.com/user-attachments/assets/8e45019f-bd94-4513-8b2f-63790ade71a0)


### **Customization**  

1. To change **node colors** or **sizes**, modify the styles in:  
   - `KnowledgeMap.vue` → `<style scoped>` section.  

2. To add or remove nodes and links, edit the `nodes` and `links` data arrays in:  
   - `KnowledgeMap.vue` → `data()` function.

---

### **Troubleshooting**  

- **Port Conflict**:  
   If the default port (8080) is already in use, Vue CLI will suggest an alternative port.  
- **Vue CLI Not Found**:  
   Ensure Vue CLI is installed globally:  
   ```bash
   npm install -g @vue/cli
   ```
- **Permission Issues**:  
   Use `sudo` when installing global packages.  
