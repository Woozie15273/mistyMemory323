Preview: https://woozie15273.github.io/mistyMemory323/

Trigger when the timeline starts on thePalette Helper layer. Otherwise, it won't find the elements in hidden <div> tags.

```
const player = GetPlayer();

// Function to copy text to clipboard
const copyToClipboard = (text) => {
    navigator.clipboard.writeText(text).then(() => {
        console.log('Text copied to clipboard');
    }).catch(error => {
        console.error('Error copying text: ', error);
    });
};

// Function to copy the aria-label content of an element to the clipboard
const copyAriaLabelContent = (modelId) => {
    const element = document.querySelector(`[data-model-id="${modelId}"]`);
    if (element) {
        const ariaLabel = element.getAttribute('aria-label');
        if (ariaLabel) {
            copyToClipboard(ariaLabel);
            player.SetVar('copyDetected', true);
            setTimeout(() => {
                player.SetVar('copyDetected', false);
            }, 1000);
        } else {
            console.error('aria-label not found');
        }
    } else {
        console.error(`Element with data-model-id="${modelId}" not found`);
    }
};

// Function to add click event listeners to elements
const addCopyListenersToElements = (modelIds) => {
    modelIds.forEach(modelId => {
        const element = document.querySelector(`[data-model-id="${modelId}"]`);
        if (element && !element.dataset.listenerAdded) {
            // Make the div element accessible and clickable
            element.setAttribute('role', 'button');
            element.style.cursor = 'pointer';
            element.addEventListener('click', () => {
                copyAriaLabelContent(modelId);
            });
            element.dataset.listenerAdded = 'true';
        } else if (!element) {
            console.error(`Element with data-model-id="${modelId}" not found`);
        }
    });
};

// List of model IDs to add listeners to
const modelIds = [
    "6O18DTLmrSp", "66YBVlhA7fE", "5jHgmfHg8eX", "61aLpz4doab",
    "5ssCC7ZPgK5", "5WydxOiuTjv", "6VIaVH9nsDv", "6mXnfGUohg4",
    "5o7d1gaROVi", "5dsoaHUmShx", "5qGuBwxoB8v", "5cV4QsVqFjl",
    "6bclf8M48ZI", "69JLHRzwmjz"
];

// Add event listeners to the elements
addCopyListenersToElements(modelIds);
```
