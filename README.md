# toa
Super simple toast to avoid loading some overkill external library


```js
export const toast = (text, type = 'success') => {
	const colors = { success: "#059669", warn: '#facc15', error: '#e11d48' };
	
	// Validate type
	if (!colors[type]) {
		console.warn(`Invalid toast type "${type}". Using default styling.`);
	}
  
	// Get or create container
	let container = document.getElementById('toast-container');
	if (!container) {
	  container = document.createElement('div');
	  container.id = 'toast-container';
	  Object.assign(container.style, {
		position: 'fixed',
		bottom: '20px',
		left: '50%',
		transform: 'translateX(-50%)',
		display: 'flex',
		flexDirection: 'column',
		gap: '10px',
		zIndex: '1000'
	  });
	  document.body.appendChild(container);
	}
  
	// Limit maximum number of toasts
	if (container.children.length >= 8) {
	  container.removeChild(container.lastChild);
	}
  
	// Create toast
	const toast = document.createElement("div");
	Object.assign(toast.style, {
	  backgroundColor: colors[type] || "#333",
	  color: "#fff",
	  padding: "10px 20px",
	  borderRadius: "5px",
	  boxShadow: "0 4px 6px rgba(0, 0, 0, 0.1)",
	  opacity: "0",
	  transition: "opacity 0.3s ease"
	});
	
	toast.innerText = text;
	container.appendChild(toast);
  
	// Show the toast
	requestAnimationFrame(() => { toast.style.opacity = "1"; });
  
	// Auto hide and remove
	setTimeout(() => {
	  toast.style.opacity = "0";
	  setTimeout(() => toast.remove(), 300);
	}, 5000);
}
```
