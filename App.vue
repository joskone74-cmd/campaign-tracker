<script setup>
const campaigns = [
  { id: 1, name: 'Нутра: Крем от боли в спине', geo: 'DE', budget: 1500, leads: 42, status: 'Active' },
  { id: 2, name: 'Гемблинг: Казино бонус 100%', geo: 'BR', budget: 3200, leads: 98, status: 'Active' },
  { id: 3, name: 'Крипта: Обучение трейдингу', geo: 'US', budget: 800, leads: 12, status: 'Paused' },
]
</script>

<template>
  <div class="container">
    <h1>Трекер кампаний</h1>

    <div class="stats-bar">
      <div>
        <span>Общий бюджет:</span>
        <strong>\${{ totalBudget }}</strong>
      </div>
      <div>
        <span>Всего лидов:</span>
        <strong>{{ totalLeads }}</strong>
      </div>
      <div>
        <span>Средний CPL:</span>
        <strong>\${{ avgCPL }}</strong>
      </div>
    </div>

    <table>
      <thead>
        <tr>
          <th>Кампания</th>
          <th>Гео</th>
          <th>Бюджет (\$)</th>
          <th>Лиды</th>
          <th>Статус</th>
          <th>CPL (\$)</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="camp in campaigns" :key="camp.id">
          <td>{{ camp.name }}</td>
          <td>{{ camp.geo }}</td>
          <td>\${{ camp.budget }}</td>
          <td>{{ camp.leads }}</td>
          <td :class="camp.status">{{ camp.status }}</td>
          <td>{{ camp.leads > 0 ? (camp.budget / camp.leads).toFixed(2) : '-' }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      campaigns: [
        { id: 1, name: 'Нутра: Крем от боли в спине', geo: 'DE', budget: 1500, leads: 42, status: 'Active' },
        { id: 2, name: 'Гемблинг: Казино бонус 100%', geo: 'BR', budget: 3200, leads: 98, status: 'Active' },
        { id: 3, name: 'Крипта: Обучение трейдингу', geo: 'US', budget: 800, leads: 12, status: 'Paused' }
      ]
    }
  },
  computed: {
    totalBudget() {
      return this.campaigns.reduce((sum, camp) => sum + camp.budget, 0);
    },
    totalLeads() {
      return this.campaigns.reduce((sum, camp) => sum + camp.leads, 0);
    },
    avgCPL() {
      const totalSpent = this.totalBudget;
      const totalLeads = this.totalLeads;
      if (totalLeads === 0) return '-';
      return (totalSpent / totalLeads).toFixed(2);
    }
  }
}
</script>

<style scoped>
.container { padding: 24px; font-family: Arial, sans-serif; }

.stats-bar {
  display: flex;
  gap: 20px;
  margin-bottom: 16px;
  padding: 12px 16px;
  background-color: #f9f9f9;
  border-radius: 8px;
  border: 1px solid #eee;
}
.stats-bar div { display: flex; flex-direction: column; }
.stats-bar span { font-size: 12px; color: #666; }
.stats-bar strong { font-size: 18px; color: #333; }

table { width: 100%; border-collapse: collapse; margin-top: 16px; }
th, td { border: 1px solid #ddd; padding: 8px 12px; text-align: left; }
th { background-color: #f5f5f5; }

.Active { color: green; font-weight: bold; }
.Paused { color: orange; font-weight: bold; }
</style>