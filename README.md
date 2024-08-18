# Youtube-pop-up-player
Frustrated with YouTube's slow loading? Use this script to play YouTube videos in a pop-up, bypassing the need to reload YouTube repeatedly.



https://github.com/user-attachments/assets/4d4a11c8-250c-4eef-b160-8f9f1d2e0ad2



```
// Function to handle video links
function handleVideoLink(link) {
    link.addEventListener('click', function(event) {
        event.stopImmediatePropagation(); // Stop other event listeners
        event.preventDefault(); // Prevent the default link behavior

        // Extract the video ID from the href
        const videoId = link.getAttribute('href').split('v=')[1];

        // Create the YouTube embed link
        const embedLink = `https://www.youtube.com/embed/${videoId}`;
        const originalLink = `https://www.youtube.com/watch?v=${videoId}`;

        // Create popup overlay
        const overlay = document.createElement('div');
        overlay.classList.add('popup-overlay');
        overlay.style.position = 'fixed';
        overlay.style.top = 0;
        overlay.style.left = 0;
        overlay.style.width = '100%';
        overlay.style.height = '100%';
        overlay.style.backgroundColor = 'rgba(0, 0, 0, 0.8)';
        overlay.style.zIndex = '9999'; // Very high z-index
        overlay.style.display = 'flex';
        overlay.style.justifyContent = 'center';
        overlay.style.alignItems = 'center';
        document.body.appendChild(overlay);

        // Create popup container
        const popup = document.createElement('div');
        popup.style.position = 'relative';
        popup.style.width = '80%';
        popup.style.height = '80%';
        popup.style.backgroundColor = '#fff';
        popup.style.borderRadius = '10px';
        popup.style.overflow = 'hidden';
        popup.style.boxShadow = '0 4px 8px rgba(0, 0, 0, 0.2)'; // Added shadow for depth
        overlay.appendChild(popup);



 // Create a container for the buttons
        const buttonContainer = document.createElement('div');
        buttonContainer.style.position = 'absolute';
        buttonContainer.style.top = '10px';
        buttonContainer.style.right = '10px';
        buttonContainer.style.display = 'flex';
        buttonContainer.style.gap = '10px';
        overlay.appendChild(buttonContainer);




        // Create iframe to show the content
        const iframe = document.createElement('iframe');
        iframe.src = embedLink;
        iframe.style.width = '100%';
        iframe.style.height = '100%';
        iframe.style.border = 'none';
        popup.appendChild(iframe);








       

        // Create the close button
        const closeButton = document.createElement('button');
        closeButton.textContent = 'close';
        closeButton.style.padding = '8px';
        closeButton.style.fontSize = '16px';
        closeButton.style.backgroundColor = '#f44336';
        closeButton.style.color = '#fff';
        closeButton.style.border = 'none';
        closeButton.style.borderRadius = '5px';
        closeButton.style.cursor = 'pointer';
        closeButton.style.boxShadow = '0 2px 4px rgba(0, 0, 0, 0.2)';
        closeButton.addEventListener('click', function() {
            document.body.removeChild(overlay); // Remove the overlay
        });
        buttonContainer.appendChild(closeButton);

        // Create the open in new tab button
        const newTabButton = document.createElement('button');
        newTabButton.textContent = ' Open in new tab';
        newTabButton.style.padding = '8px';
        newTabButton.style.fontSize = '16px';
        newTabButton.style.backgroundColor = '#008CBA';
        newTabButton.style.color = '#fff';
        newTabButton.style.border = 'none';
        newTabButton.style.borderRadius = '5px';
        newTabButton.style.cursor = 'pointer';
        newTabButton.style.boxShadow = '0 2px 4px rgba(0, 0, 0, 0.2)';
        newTabButton.addEventListener('click', function() {
            window.open(originalLink, '_blank');
        });
        buttonContainer.appendChild(newTabButton);
    });
}

// Function to add listeners to existing and dynamically added video links
function addListenersToLinks() {
    document.querySelectorAll('#video-title-link').forEach(function(link) {
        handleVideoLink(link);
    });
}

// Use MutationObserver to detect dynamically added elements
const observer = new MutationObserver(function(mutations) {
    mutations.forEach(function(mutation) {
        mutation.addedNodes.forEach(function(node) {
            if (node.nodeType === 1 && node.matches('#video-title-link')) {
                handleVideoLink(node);
            }
            if (node.nodeType === 1) {
                addListenersToLinks(); // Handle nested nodes
            }
        });
    });
});

// Start observing the document for changes
observer.observe(document.body, {
    childList: true,
    subtree: true
});

// Add listeners to links that already exist on the page
addListenersToLinks();

```






# Tampermonkey User Script Installation Guide

This guide will help you install and use a third-party user script with Tampermonkey on your browser.

## What is Tampermonkey?

[Tampermonkey](https://www.tampermonkey.net/) is a popular userscript manager that allows you to run custom scripts to modify webpages. These scripts can enhance your browsing experience by adding new features, removing unwanted elements, or automating tasks.

## Step-by-Step Installation Guide

### 1. Install Tampermonkey

#### **For Google Chrome:**

1. Visit the Chrome Web Store.
2. Click the **"Add to Chrome"** button.
3. Confirm the installation by clicking **"Add Extension"** in the pop-up.

#### **For Firefox:**

1. Visit the [Firefox Add-ons Store](https://addons.mozilla.org/firefox/addon/tampermonkey/).
2. Click the **"Add to Firefox"** button.
3. Confirm the installation by clicking **"Add"** in the pop-up.

#### **For Microsoft Edge:**

1. Visit the [Microsoft Edge Add-ons Store](https://microsoftedge.microsoft.com/addons/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo).
2. Click the **"Get"** button.
3. Confirm the installation by clicking **"Add Extension"** in the pop-up.

#### **For Safari:**

1. Visit the [Mac App Store](https://apps.apple.com/app/tampermonkey/id1482490089) and search for "Tampermonkey."
2. Click the **"Get"** button and follow the prompts to install.

#### **For Opera:**

1. Visit the Opera Add-ons Store.
2. Click the **"Add to Opera"** button.
3. Confirm the installation by clicking **"Install"** in the pop-up.

### 2. Add a Third-Party User Script

Once Tampermonkey is installed, you can add the third-party user script.

1. **Find a Script:**
    
    - Obtain the URL of the script or download the script file.
    - Make sure you trust the source of the script, as it can have significant access to your browsing.
2. **Install the Script:**
    
    - Open the Tampermonkey dashboard by clicking the Tampermonkey icon in your browser toolbar and selecting **"Dashboard"**.
    - Click the **"+"** icon to create a new script, or if you have a URL:
        - Click the **"Utilities"** tab.
        - Paste the script URL in the "Install from URL" field.
        - Click **"Install"**.
    - If you have a script file, click **"Choose File"** under the "File import" section, then **"Import"**.
3. **Configure the Script (Optional):**
    
    - Some scripts might have settings that can be configured in the Tampermonkey dashboard. Review any provided documentation for the script.
4. **Enable the Script:**
    
    - Ensure the script is enabled by checking the checkbox next to its name in the Tampermonkey dashboard.

### 3. Use the Script

1. **Visit the Target Website:**
    
    - Go to the website where the script is supposed to run.
    - Tampermonkey will automatically execute the script when you visit the relevant pages.
2. **Manage the Script:**
    
    - If you need to disable, edit, or remove the script, return to the Tampermonkey dashboard, find the script in the list, and use the available options.

### 4. Updating the Script

1. **Automatic Updates:**
    
    - Tampermonkey can automatically check for updates if the script's metadata includes a valid update URL.
2. **Manual Updates:**
    
    - You can manually update the script by finding its source or URL and reinstalling it following the same steps above.

## Troubleshooting

- **Script Not Working?**
    
    - Check that the script is enabled.
    - Ensure you are on the correct website or page.
    - Clear your browser cache and try again.
- **Conflicts with Other Extensions:**
    
    - Disable other extensions temporarily to see if they are interfering with the script.
- **Contact Script Author:**
    
    - If you have issues specific to the script, contact the author or check the support forums for help.

## Safety Notice

Always be cautious when installing third-party scripts, especially those from untrusted sources. Scripts have access to your browser and can collect data or perform actions on your behalf.

## Additional Resources

- Tampermonkey Documentation
- [User Scripts on Greasy Fork](https://greasyfork.org/)
