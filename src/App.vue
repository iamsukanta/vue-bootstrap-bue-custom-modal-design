<template>
  <b-container>
    <b-row>
      <b-col class="text-center p-5">
        <b-button v-b-modal.notification-modal>Open Modal</b-button>
        <b-modal ref="notification-modal" id="notification-modal"  hide-footer hide-header>
          <div class="notification-content">
            <div class="notification-header">
              <b-row>
                <b-col class="text-center">
                  <h5 class="mb-0">Notifications</h5>
                  <span @click="closeModal" class="modal-close">&times;</span>
                </b-col>
              </b-row>
            </div>

            <div class="notification-body">
              <div class="notification-item">
                <div class="item-box p-2">
                  <b-row v-for="(notification, index) in notifications" :key="index" class="mb-2">
                    <b-col>
                      <div class="item p-2">
                        <div class="item-inner position-relative" v-bind:class="colorBindingClass(notification.status)">
                          <h6 class="title">{{ notification.title }}</h6>
                          <small>{{ notification.text }}</small>
                          <span class="notification-time">{{ notification.time }}</span>
                        </div>
                      </div>
                    </b-col>
                  </b-row>
                </div>
              </div>
            </div>
          </div>
        </b-modal>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      notifications: [
        { title: 'Deposit Confirmed', text: 'Lorem, ipsum dolor sit amet consectetur.', time: '10.40', status: 1 },
        { title: 'Deposit Pending', text: 'Lorem, ipsum dolor sit amet consectetur.', time: '14.30', status: 2 },
        { title: 'Withdrawl Confirmed', text: 'Lorem, ipsum dolor sit amet consectetur.', time: '11.40', status: 3 },
        { title: 'Withdrawl Pending', text: 'Lorem, ipsum dolor sit amet consectetur.', time: '10.50', status: 2 },
        { title: 'Tip Received', text: 'Lorem, ipsum dolor sit amet consectetur.', time: '17.20', status: 4 },
        { title: 'Game #4324 result won', text: 'Lorem, ipsum dolor sit amet consectetur.', time: '10.40', status: 1 },
        { title: 'Game #5324 result lost', text: 'Lorem, ipsum dolor sit amet consectetur.', time: '08.10', status: 3 },
        { title: 'Deposit Confirmed', text: 'Lorem, ipsum dolor sit amet consectetur.', time: '10.40', status: 1 },
        { title: 'Deposit Pending', text: 'Lorem, ipsum dolor sit amet consectetur.', time: '14.30', status: 2 },
        { title: 'Withdrawl Confirmed', text: 'Lorem, ipsum dolor sit amet consectetur.', time: '11.40', status: 3 },
        { title: 'Withdrawl Pending', text: 'Lorem, ipsum dolor sit amet consectetur.', time: '10.50', status: 2 },
        { title: 'Tip Received', text: 'Lorem, ipsum dolor sit amet consectetur.', time: '17.20', status: 4 },
        { title: 'Game #4324 result won', text: 'Lorem, ipsum dolor sit amet consectetur.', time: '10.40', status: 1 },
        { title: 'Game #5324 result lost', text: 'Lorem, ipsum dolor sit amet consectetur.', time: '10.40', status: 3 }
      ]
    }
  },
  methods: {
    closeModal() {
      this.$refs['notification-modal'].hide();
    },
    colorBindingClass(status) {
      switch(status) {
        case 1:
          return 'color-green';
        case 2:
          return 'color-white';
        case 3:
          return 'color-yellow';
        case 4:
          return 'color-red';       
        default:
          return 'color-white';  
      }
    }
  }
}
</script>

<style lang="scss">
  #notification-modal {
    .modal-content {
      background-color: #252233;
      border-radius: 20px;
      .modal-body {
        padding: 0px !important;
        .notification-content {
          .notification-header {
            background-color: #1D1A2A;
            color: #FFFFFF;
            border-radius: 20px 20px 0px 0px;
            padding: 15px;
            .modal-close {
              color: #FF4A4A;
              position: absolute;
              right: 15px;
              top: 7px;
              font-size: 25px;
              cursor: pointer;
            }
          }

          .notification-body {
            padding: 15px;
            
            .notification-item {
             
              background-color: #1C1927;
              border: 1px solid #5417B1;
              padding: 10px;
              padding-left: 0px;
              border-radius: 10px;

              .item-box {
                height: 400px;
                overflow-y: scroll;
                overflow-x: hidden;

                .item {
                  background-color: #262333;
                  padding: 3px;
                  border-radius: 5px;

                  .item-inner {
                    border-left: 2px solid #5417B1;
                    color: #79758A;
                    padding: 3px;
                    padding-left: 8px;
                    line-height: 0.7rem;
                    .title {
                      margin-bottom: 0px !important;
                      font-size: 14px !important;
                      color: #5417B1;
                      margin-top: -3px;
                    }
                    small {
                      font-size: 12px !important;
                    }

                    .notification-time {
                      position: absolute;
                      right: 0px;
                      top: 0px;
                      font-size: 10px;
                    }
                  }

                  .color-green {
                    border-left: 2px solid #79F591;
                    .title {
                      color: #79F591;
                    }
                  }

                  .color-white {
                    border-left: 2px solid #FFFFFF;
                    .title {
                      color: #FFFFFF;
                    }
                  }

                  .color-yellow {
                    border-left: 2px solid #FFA30F;
                    .title {
                      color: #FFA30F;
                    }
                  }

                  .color-red {
                    border-left: 2px solid #FF1C61;
                    .title {
                      color: #FF1C61;
                    }
                  }
                }
              }

              .item-box::-webkit-scrollbar {
                width: 4px;
              }

              .item-box::-webkit-scrollbar-track {
                background: #1C1927;
              }

              .item-box::-webkit-scrollbar-thumb {
                border-radius: 1rem;
                background-color: #5417B1;
              }
                
            }  
          }
        }
      }
    }
  }
</style>

