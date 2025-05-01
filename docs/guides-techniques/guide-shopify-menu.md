# Shopify Templates, Pages, and Menus: Best Practices

When building a Shopify website, it’s crucial to properly structure templates, pages, and menus to ensure flexibility and maintainability. This document outlines **why** we use unique templates for pages and **how** to implement them.

---

## **Why Use Unique Templates for Pages?**
1. **Avoid Shared Customizations:**  
   If multiple pages share the same template, any changes to that template will affect all the pages using it. This can lead to unintended design or content changes.
   
2. **Maintain Flexibility:**  
   Unique templates allow each page to have its own structure, design, and content, making it easier to customize the user experience.

3. **Improve Scalability:**  
   Having a structured setup simplifies adding new pages, templates, or menu items in the future.

---

## **Key Steps for Structuring a Shopify Website**

### **Step 1: Create a Template for Each Page**
- Navigate to your theme's code using **Online Store > Themes > Edit Code**.
- Under the **Templates** directory, create a new template for each unique page.
  - For example:
    - `page.nos-services.liquid`
    - `page.nos-realisations.liquid`
- If necessary, create unique sections under the **Sections** directory for additional customization.

---

### **Step 2: Create a Page for Each Template**
- Go to **Online Store > Pages** in the Shopify Admin.
- Create a new page for each unique template (e.g., "Nos Services" and "Nos Réalisations").
- Assign the correct template to the page:
  - In the page editor, use the **Theme Template** dropdown to select the corresponding template (e.g., `page.nos-services` for "Nos Services").

---

### **Step 3: Build Your Menu**
- Go to **Online Store > Navigation**.
- Add links to your menu that point to the newly created pages:
  - For "Nos Services," link to the page assigned to `page.nos-services`.
  - For "Nos Réalisations," link to the page assigned to `page.nos-realisations`.

---

## **Pro Tips**
- **Use Descriptive Template Names:**  
  Name your templates logically (e.g., `page.services.liquid`, `page.projects.liquid`) to make it clear which page they belong to.
  
- **Preview Before Publishing:**  
  Always preview your theme and menu changes in the Shopify editor to ensure everything is working as expected.

- **Follow a Consistent Workflow:**  
  1. Create the template.
  2. Assign it to a page.
  3. Link the page to your menu.

---

## **Benefits of This Workflow**
- Ensures clean and organized code.
- Prevents cross-page issues caused by shared templates.
- Provides better control over design and layout for each page.
- Makes the website easier to scale and maintain over time.

---

By following this structure, your Shopify store will be more modular, scalable, and easier to manage for both developers and non-technical users.





# Shopify Templates, Pages, and Menus: Best Practices

When building a Shopify website, it’s important to structure templates, pages, and menus correctly to avoid unnecessary issues and maintain flexibility. This document explains **why** we use unique templates for pages and **how** to set them up using Shopify's Admin UI (no coding required!).

---

## **Why Use Unique Templates for Pages?**
1. **Avoid Shared Changes:**  
   If multiple pages share the same template, any changes to one page will also affect the others. This can cause accidental layout or content issues.

2. **Keep Pages Unique:**  
   Assigning unique templates to each page ensures each page can have its own look, feel, and content.

3. **Scale Easily:**  
   Following this structure makes it easier to add or edit pages and menus in the future without breaking other parts of the site.

---

## **Key Steps for Structuring a Shopify Website**

### **Step 1: Create a Unique Template for Each Page**
Templates determine how pages look. Shopify provides default templates, but you can create new ones for custom layouts.

To create a unique template:
1. Go to **Online Store > Themes** in your Shopify Admin.
2. Find your live theme and click **Customize**.
3. From the customization screen:
   - Open the dropdown at the top of the screen (it may say "Home Page").
   - Select **Pages** > **Create template**.
4. Name the new template (e.g., `Nos Services` or `Nos Réalisations`) and click **Create Template**.

Now, you have a template that can be customized independently from other pages.

---

### **Step 2: Create a Page for Each Template**
Once the templates are created, assign them to individual pages:

1. Go to **Online Store > Pages** in your Shopify Admin.
2. Click **Add Page** to create a new page for each template.
   - For example:
     - Page Title: "Nos Services"
     - Page Title: "Nos Réalisations"
3. At the bottom right of the page editor, look for the **Theme Template** dropdown.
4. Select the corresponding template you created (e.g., `page.nos-services` for "Nos Services").
5. Click **Save**.

Repeat this process for each page that requires a unique layout or design.

---

### **Step 3: Link Pages to Your Menu**
To make these pages accessible from your website’s navigation menu:

1. Go to **Online Store > Navigation** in your Shopify Admin.
2. Click the menu where you want the pages to appear (e.g., the **Main Menu**).
3. Click **Add Menu Item** to create a new menu link:
   - Name: "Nos Services"
   - Link: Select **Pages** > **Nos Services**
4. Repeat this process for the other page (e.g., "Nos Réalisations").
5. Save the menu.

Now, the pages will appear in your website’s navigation menu, each with its own unique template and layout.

---

## **Pro Tips**
- **Use Clear Names for Templates and Pages:**  
   Always name templates and pages descriptively (e.g., "Nos Services" instead of "Page 1") to keep your site organized.

- **Preview Before Publishing:**  
   Use the **Customize** tool under **Online Store > Themes** to preview pages and menus before publishing.

- **Keep It Simple:**  
   If you’re not sure how to structure a page or template, start with Shopify’s defaults and customize later.

---

## **Benefits of This Workflow**
- Each page can have its own unique layout and content.
- Changes made to one page won’t affect other pages.
- The website will be easier to scale and maintain over time.

---

By following these steps, your Shopify website will stay organized, easy to manage, and flexible for future changes. No coding required!



