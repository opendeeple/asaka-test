<template>
  <header>
    
  </header>
  <main>
    <ol v-draggable="[list, {animation: 150}]" class="list">
      <li class="list-item" v-for="(item, index) in list" v-bind:key="index">
        <div class="list-item-heading">
          <!-- number column -->
          <div class="list-item-number">
            <div class="list-item-header">
              №
            </div>
            <div class="list-item-body">
              {{ index + 1 }}
            </div>
          </div>
          <!-- name column -->
          <div class="list-item-name">
            <div class="list-item-header">
              Название
            </div>
            <div class="list-item-body">
              <img src="~@/assets/icons/folder-icon.svg"/> {{ item.name }}
            </div>
          </div>

          <!-- inorder column -->
          <div class="list-item-in-order">
            <div class="list-item-header">
              Очередность
            </div>
            <div class="list-item-body">
              {{ item.inorder }}
            </div>
          </div>

          <!-- category column -->
          <div class="list-item-subcategory">
            <div class="list-item-header">
              Подкатегории
            </div>
            <div class="list-item-body">
              {{ toCategoryString(item.category) }}
            </div>
          </div>

          <!-- tools column -->
          <div class="list-item-tools">
            <div class="indicator">
              <img src="~@/assets/icons/dots.svg" alt="dots">
            </div>
            <DropdownMenu />
            <div class="badge">{{ item.badgeNumber }}</div>
          </div>
        </div>

        <!-- subitems -->
        <ol class="sublist" v-if="item.items" tag="ol">
          <li class="list-subitem" v-for="(item, subindex) in item.items" v-bind:key="subindex">
            <div class="sublist-divider" v-if="subindex != 0" />
            <div class="list-item-row">
              <!-- subitem number column -->
              <div class="list-item-number">
                <div class="list-item-header">
                  №
                </div>
                <div class="list-item-body">
                  {{ index + 1 }}.{{ subindex + 1 }}
                </div>
              </div>
              <!-- subitem name column -->
              <div class="list-item-name">
                <div class="list-item-header">
                  Название
                </div>
                <div class="list-item-body">
                  <img src="~@/assets/icons/file-icon.svg"/> {{ item.name }}
                </div>
              </div>
              <!-- subitem inorder column -->
              <div class="list-item-in-order">
                <div class="list-item-header">
                  Очередность
                </div>
                <div class="list-item-body">
                  {{ item.inorder }}
                </div>
              </div>
              <!-- subitem tools -->
              <div class="list-item-tools">
                <div class="indicator">
                  <img src="~@/assets/icons/dots.svg" alt="dots">
                </div>
              </div>
            </div>
          </li>
        </ol>
      </li>
    </ol>
  </main>
</template>

<script setup>
import { ref } from 'vue'
import DropdownMenu from "@/components/DropdownMenu.vue"
import { vDraggable } from 'vue-draggable-plus'

const list = ref([
{ 
  name: "Mastercard", 
  inorder: 1,
  category: [
    "Mastercard (Standart)",
    "Mastercard (World)",
    "Mastercard (Platinum)",
    "Mastercard (Gold)",
    "Master card"
      ],
      badgeNumber: 12
    },
    {
      name: "вклады",
      inorder: 2,
      category: [
        "Максимал фойда (Нац. валюта)",
        "On-line (Нац. валюта)",
        "Аванс (Нац. валюта)",
        "Максимал фойда"
      ],
      badgeNumber: 9,
      items: [
        {
          name: "Максимал фойда (Нац. валюта)",
          inorder: 1
        },
        {
          name: "On-line (Нац. валюта)",
          inorder: 2
        },
        {
          name: "Аванс (Нац. валюта)",
          inorder: 3
        },
        {
          name: "Максимал фойда (Ин. валюта)",
          inorder: 4
        },
        {
          name: "On-line (Ин. валюта)",
          inorder: 5
        },
        {
          name: "Аванс (Ин. валюта)",
          inorder: 6
        }
      ]
    },
    {
      name: "Кредиты",
      inorder: 3,
      category: [],
      badgeNumber: 12
    }
  ]
)

function toCategoryString(category) {
  if (category.length == 0) {
    return "-"
  }
  return category.join(" / ")
}

</script>