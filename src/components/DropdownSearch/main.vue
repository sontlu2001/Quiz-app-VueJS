<template>
  <div class="form-group">
    <div class="dropdown">
      <div class="dropdown-select">Select your country</div>
      <div class="dropdown-menu" style="display: block">
        <input
          placeholder="Search..."
          type="text"
          class="dropdown-menu-search" />
        <div class="dropdown-menu-inner">
          <div
            class="dropdown-menu-item selected"
            data-value="Select your country">
            Select your country
          </div>
          <div class="dropdown-menu-item" data-value="Afghanistan">
            Afghanistan
          </div>
          <div class="dropdown-menu-item" data-value="Albania">Albania</div>
          <div class="dropdown-menu-item" data-value="Algeria">Algeria</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script src="./index.js"></script>

<style src="./style.scss" lang="scss" scoped></style>
