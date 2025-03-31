<template>
    <div>
      <!-- ปุ่มเปิด Sidebar -->
      <button class="menu-btn" @click="toggleSidebar">
        ☰ เมนู
      </button>
  
      <!-- Sidebar -->
      <div :class="['sidebar', { 'active': isOpen }]">
        <div class="sidebar-header">
          <h2>เมนูหลัก</h2>
          <button class="close-btn" @click="toggleSidebar">✖</button>
        </div>
        
        <ul>
          <li><a href="#">🏠 หน้าหลัก</a></li>
          <li><a href="https://mail.google.com/mail/u/0/#inbox"> GMAIL</a></li>
          <li><a href="https://www.facebook.com/kpz.castgaming.5?locale=th_TH">👤FACEBOOK</a></li>

        </ul>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        isOpen: false
      };
    },
    methods: {
      toggleSidebar() {
        this.isOpen = !this.isOpen;
        this.$emit('toggleSidebar', this.isOpen);
      }
    }
  };
  </script>
  
  <style scoped>

  .menu-btn {
    position: fixed;
    top: 20px;
    left: 20px;
    background: rgba(0, 0, 0, 0.6);
    color: white;
    border: none;
    padding: 12px 18px;
    border-radius: 8px;
    cursor: pointer;
    font-size: 18px;
    transition: background 0.3s;
  }
  
  .menu-btn:hover {
    background: rgba(0, 0, 0, 0.8);
  }
  

  .sidebar {
    position: fixed;
    top: 0;
    left: -250px;
    width: 250px;
    height: 100%;
    background: rgba(255, 255, 255, 0.15);
    backdrop-filter: blur(12px);
    box-shadow: 4px 0 10px rgba(0, 0, 0, 0.2);
    transition: left 0.3s ease-in-out;
    padding-top: 60px;
  }
  
  .sidebar.active {
    left: 0;
  }

  .sidebar-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
    color: white;
  }
  
  .sidebar-header h2 {
    font-size: 20px;
    margin: 0;
  }
  
  .close-btn {
    background: none;
    border: none;
    font-size: 22px;
    color: white;
    cursor: pointer;
    transition: transform 0.3s ease;
  }
  
  .close-btn:hover {
    transform: rotate(90deg);
  }
  
  .sidebar ul {
    list-style: none;
    padding: 0;
  }
  
  .sidebar ul li {
    padding: 15px;
    text-align: center;
  }
  
  .sidebar ul li a {
    text-decoration: none;
    color: white;
    font-size: 18px;
    display: block;
    transition: background 0.3s ease;
  }
  
  .sidebar ul li a:hover {
    background: rgba(255, 255, 255, 0.3);
    border-radius: 8px;
  }
  </style>
  