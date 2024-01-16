<script>
    export let title = "Two Sections Example";
  </script>
  
  <style>
    .grid-container {
      display: grid;
      grid-template-columns: 1fr 1fr; /* Two equal columns */
      gap: 4; /* Adjust the gap as needed */
    }
  
    .section {
      padding: 4; /* Adjust the padding as needed */
      border: 1px solid #ccc; /* Optional: Add a border for visual separation */
    }
  </style>
  
  <main>
    <div class="grid-container">
      <!-- First Section -->
      <div class="section">
        <h2 class="text-xl font-bold mb-2">Section 1</h2>
        <!-- Your content for Section 1 goes here -->
        <p>This is the content of the first section.</p>
      </div>
  
      <!-- Second Section -->
      <div class="section">
        <h2 class="text-xl font-bold mb-2">Section 2</h2>
        <!-- Your content for Section 2 goes here -->
        <p>This is the content of the second section.</p>
      </div>
    </div>
  </main>
  