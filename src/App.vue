<template>
  <div id="app">
      <el-tooltip content="Click on any of the cells or on the edit button to edit content">
       <i class="el-icon-info"></i>
      </el-tooltip>
       <el-table
      :data="gridData"
      style="width: 100%">

       <el-table-column
        label="Operations"
        min-width="180">
        <template slot-scope="{row, index}">
         <el-button icon="el-icon-edit"
          @click="setEditMode(row, index)">
        </el-button>
         <el-button type="success" icon="el-icon-check"
          @click="saveRow(row, index)">
        </el-button>
        </template>
      </el-table-column>


      <el-table-column
        label="Name"
        min-width="180">
        <editable-cell :show-input="row.editMode" slot-scope="{row}" v-model="row.name">
          <span slot="content">{{row.name}}</span>
        </editable-cell>
      </el-table-column>

      <el-table-column
        min-wwidth="150"
        label="Gender">

         <editable-cell 
         :show-input="row.editMode"
         slot-scope="{row}" 
         editable-component="el-select"
         close-event="change"
         v-model="row.gender">
         
          <el-tag size="medium" 
                  :type="row.gender === 'M' ? 'primary' : 'danger'" 
                  slot="content">
                  {{row.gender === 'M' ? 'Male': 'Female'}}
          </el-tag>

          <template slot="edit-component-slot">
            <el-option value="M" label="Male"></el-option>
            <el-option value="F" label="Female"></el-option>
          </template>
        </editable-cell>
        
      </el-table-column>


      <el-table-column
        label="Birth Date"
        min-width="250">
         <editable-cell 
         :show-input="row.editMode"
         slot-scope="{row}" 
         editable-component="el-date-picker"
         format="yyyy-MM-dd"
         value-format="yyyy-MM-dd"
         v-model="row.date">
          <span slot="content">{{row.date}}</span>
        </editable-cell>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import EditableCell from "./components/EditableCell.vue";

export default {
  name: "App",
  components: {
    EditableCell
  },
  data() {
    return {
      gridData: [
        {
          date: "2016-05-03",
          name: "Tom",
          gender: "M"
        },
        {
          date: "2016-05-02",
          name: "Lisa",
          gender: "F"
        },
        {
          date: "2016-05-04",
          name: "Jon",
          gender: "M"
        },
        {
          date: "2016-05-01",
          name: "Mary",
          gender: "F"
        }
      ]
    };
  },
  methods: {
    setEditMode(row, index) {
      row.editMode = true;
    },
    saveRow(row, index) {
      row.editMode = false;
    }
  },
  mounted() {
    this.gridData = this.gridData.map(row => {
      return {
        ...row,
        editMode: false
      };
    });
  }
};
</script>

<style>
.edit-cell {
  min-height: 35px;
  cursor: pointer;
}
</style>
