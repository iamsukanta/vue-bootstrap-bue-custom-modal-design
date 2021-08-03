<template>
  <b-container>
    <b-row>
      <b-col class="p-5">
        <b-button v-b-modal.notification-modal class="me-3">Notification modal</b-button>
        <b-button v-b-modal.staff-online-modal class="me-3">Staff Online</b-button>
        <b-button v-b-modal.coinflip-match-modal class="me-3">Coinflip Match</b-button>

        <!-- Notification Modal -->
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

        <!-- Staff Online Modal -->
        <b-modal ref="staff-online-modal" id="staff-online-modal"  hide-footer hide-header>
          <div class="staff-online-content">
            <div class="staff-online-header">
              <b-row>
                <b-col class="text-center">
                  <h5 class="mb-0">Staff Online</h5>
                  <span @click="closeStaffModal" class="modal-close">&times;</span>
                </b-col>
              </b-row>
            </div>

            <div class="staff-online-body">
              <span class="content-title"> <span v-if="onlineUser" @click="onlineUser = !onlineUser" class="cursor-pointer">-</span> <span v-if="!onlineUser" @click="onlineUser = !onlineUser" class="cursor-pointer">+</span> Online ({{ onlineUsers.length }})</span><br/>
              <div v-if="onlineUser" class="online-user-content">
                <b-row class="mt-2" v-for="(user, index) in onlineUsers" :key="index">
                  <b-col>
                    <div class="content-box position-relative" v-bind:class="staffOnlineColorBindingClass(user.status)">
                        <svg id="contentBoxSvgIcon" class="content-box-svg-icon" xmlns="http://www.w3.org/2000/svg" width="11.047" height="12.477" viewBox="0 0 11.047 12.477">
                          <path id="XMLID_88_" d="M126.76,4.279A5.375,5.375,0,0,1,135.076.955l.25.173-.44.987a4.8,4.8,0,0,0-1.981-.409,4.667,4.667,0,0,0-.556.033V1.18h-.733v.707a4.619,4.619,0,0,0-1.263.585l-.488-.633-.581.448.491.637a4.673,4.673,0,0,0-.824,1l-.728-.212-.205.7.6.174a4.614,4.614,0,0,0-.346,1.757v.769h-1.338l-.076-.266a5.385,5.385,0,0,1-.092-2.569Z" transform="translate(-126.647 0)" fill="#ff1c61"/>
                          <path id="XMLID_90_" d="M74.493,103.681A3.91,3.91,0,0,1,78.4,99.775a4.073,4.073,0,0,1,3.718,2.35,5.687,5.687,0,0,1-2.241,1.252A1.353,1.353,0,1,0,78.34,105.6a2.171,2.171,0,0,0-.59,1.153,5.4,5.4,0,0,1-1.337,2.954l-.107.107h-.649a2.487,2.487,0,0,1-1.05-.23,2.521,2.521,0,0,1-.858-.649l-.18-.21.153-.23a3.6,3.6,0,0,0,.77-2.207Z" transform="translate(-72.141 -97.337)" fill="#ff1c61"/>
                          <path id="XMLID_107_" d="M31.062,202.09a1.348,1.348,0,0,0-.071-.433,6.486,6.486,0,0,0,2.646-1.683l.007-.008.086-.094.007.053.023.178c.044.342.072.574.087.786A11.025,11.025,0,0,1,33.8,202.4l-.024.362-.219,0a2.031,2.031,0,0,0-1.3.51,1.642,1.642,0,0,0-.45,1.153l.148,1.7a1.975,1.975,0,0,1-.593.187,3.441,3.441,0,0,1-.737,0l-.87-2.725v-.144A1.356,1.356,0,0,0,31.062,202.09Z" transform="translate(-22.811 -194.987)" fill="#ff1c61"/>
                          <path id="XMLID_109_" d="M174.776,266.447a.621.621,0,1,1,.621-.621A.622.622,0,0,1,174.776,266.447Z" transform="translate(-167.879 -258.723)" fill="#ff1c61"/>
                        </svg>
                        <span class="ps-2 title">{{ user.title }}</span>
                        <span class="message-icon" v-if="index == 0">
                          <svg xmlns="http://www.w3.org/2000/svg" width="18.132" height="17" viewBox="0 0 18.132 17">
                            <g id="chat" transform="translate(0 -15.988)">
                              <g id="Group_47" data-name="Group 47" transform="translate(0 15.988)">
                                <g id="Group_46" data-name="Group 46" transform="translate(0 0)">
                                  <path id="Path_246" data-name="Path 246" d="M13.351,15.988H1.594A1.6,1.6,0,0,0,0,17.582v8.5a1.6,1.6,0,0,0,1.594,1.594H3.187v2.656a.532.532,0,0,0,.907.376L6.97,27.831a.53.53,0,0,1,.376-.156h6.006a1.6,1.6,0,0,0,1.594-1.594v-8.5A1.6,1.6,0,0,0,13.351,15.988Zm-10.7,3.187h7.508a.531.531,0,1,1,0,1.062H2.656a.531.531,0,0,1,0-1.062Zm5.383,5.312H2.656a.531.531,0,1,1,0-1.062H8.039a.531.531,0,1,1,0,1.062Zm4.25-2.125H2.656a.531.531,0,0,1,0-1.062h9.633a.531.531,0,1,1,0,1.062Z" transform="translate(0 -15.988)" fill="#fff"/>
                                </g>
                              </g>
                              <g id="Group_49" data-name="Group 49" transform="translate(6.503 18.113)">
                                <g id="Group_48" data-name="Group 48" transform="translate(0 0)">
                                  <path id="Path_247" data-name="Path 247" d="M193.666,75.989h-.524v7.968a2.665,2.665,0,0,1-2.663,2.656h-5.715l-1.133,1.055h4.5l3.032,3.039a.531.531,0,0,0,.907-.376V87.669h1.594a1.589,1.589,0,0,0,1.594-1.587v-8.5A1.6,1.6,0,0,0,193.666,75.989Z" transform="translate(-183.631 -75.989)" fill="#fff"/>
                                </g>
                              </g>
                            </g>
                          </svg>
                        </span>
                        <span class="status-icon">
                          <svg xmlns="http://www.w3.org/2000/svg" width="10" height="10" viewBox="0 0 10 10">
                            <circle id="Ellipse_100" data-name="Ellipse 100" cx="5" cy="5" r="5" fill="#79f591"/>
                          </svg>
                        </span>
                    </div>
                  </b-col>
                </b-row>
              </div>
              
              <br/>
              <span class="content-title"> <span v-if="!onlineUser" @click="onlineUser = !onlineUser" class="cursor-pointer">-</span> <span @click="onlineUser = !onlineUser" v-if="onlineUser" class="cursor-pointer">+</span> Offline ({{ offlineUsers.length }})</span>
              <div v-if="!onlineUser" class="offline-user-content">
                <b-row  class="mt-2" v-for="(user, index) in offlineUsers" :key="index">
                  <b-col>
                    <div class="content-box position-relative" v-bind:class="staffOnlineColorBindingClass(user.status)">
                        <svg id="contentBoxSvgIcon" class="content-box-svg-icon" xmlns="http://www.w3.org/2000/svg" width="11.047" height="12.477" viewBox="0 0 11.047 12.477">
                          <path id="XMLID_88_" d="M126.76,4.279A5.375,5.375,0,0,1,135.076.955l.25.173-.44.987a4.8,4.8,0,0,0-1.981-.409,4.667,4.667,0,0,0-.556.033V1.18h-.733v.707a4.619,4.619,0,0,0-1.263.585l-.488-.633-.581.448.491.637a4.673,4.673,0,0,0-.824,1l-.728-.212-.205.7.6.174a4.614,4.614,0,0,0-.346,1.757v.769h-1.338l-.076-.266a5.385,5.385,0,0,1-.092-2.569Z" transform="translate(-126.647 0)" fill="#ff1c61"/>
                          <path id="XMLID_90_" d="M74.493,103.681A3.91,3.91,0,0,1,78.4,99.775a4.073,4.073,0,0,1,3.718,2.35,5.687,5.687,0,0,1-2.241,1.252A1.353,1.353,0,1,0,78.34,105.6a2.171,2.171,0,0,0-.59,1.153,5.4,5.4,0,0,1-1.337,2.954l-.107.107h-.649a2.487,2.487,0,0,1-1.05-.23,2.521,2.521,0,0,1-.858-.649l-.18-.21.153-.23a3.6,3.6,0,0,0,.77-2.207Z" transform="translate(-72.141 -97.337)" fill="#ff1c61"/>
                          <path id="XMLID_107_" d="M31.062,202.09a1.348,1.348,0,0,0-.071-.433,6.486,6.486,0,0,0,2.646-1.683l.007-.008.086-.094.007.053.023.178c.044.342.072.574.087.786A11.025,11.025,0,0,1,33.8,202.4l-.024.362-.219,0a2.031,2.031,0,0,0-1.3.51,1.642,1.642,0,0,0-.45,1.153l.148,1.7a1.975,1.975,0,0,1-.593.187,3.441,3.441,0,0,1-.737,0l-.87-2.725v-.144A1.356,1.356,0,0,0,31.062,202.09Z" transform="translate(-22.811 -194.987)" fill="#ff1c61"/>
                          <path id="XMLID_109_" d="M174.776,266.447a.621.621,0,1,1,.621-.621A.622.622,0,0,1,174.776,266.447Z" transform="translate(-167.879 -258.723)" fill="#ff1c61"/>
                        </svg>
                        <span class="ps-2 title">{{ user.title }}</span>
                        <span class="message-icon" v-if="index == 0">
                          <svg xmlns="http://www.w3.org/2000/svg" width="18.132" height="17" viewBox="0 0 18.132 17">
                            <g id="chat" transform="translate(0 -15.988)">
                              <g id="Group_47" data-name="Group 47" transform="translate(0 15.988)">
                                <g id="Group_46" data-name="Group 46" transform="translate(0 0)">
                                  <path id="Path_246" data-name="Path 246" d="M13.351,15.988H1.594A1.6,1.6,0,0,0,0,17.582v8.5a1.6,1.6,0,0,0,1.594,1.594H3.187v2.656a.532.532,0,0,0,.907.376L6.97,27.831a.53.53,0,0,1,.376-.156h6.006a1.6,1.6,0,0,0,1.594-1.594v-8.5A1.6,1.6,0,0,0,13.351,15.988Zm-10.7,3.187h7.508a.531.531,0,1,1,0,1.062H2.656a.531.531,0,0,1,0-1.062Zm5.383,5.312H2.656a.531.531,0,1,1,0-1.062H8.039a.531.531,0,1,1,0,1.062Zm4.25-2.125H2.656a.531.531,0,0,1,0-1.062h9.633a.531.531,0,1,1,0,1.062Z" transform="translate(0 -15.988)" fill="#fff"/>
                                </g>
                              </g>
                              <g id="Group_49" data-name="Group 49" transform="translate(6.503 18.113)">
                                <g id="Group_48" data-name="Group 48" transform="translate(0 0)">
                                  <path id="Path_247" data-name="Path 247" d="M193.666,75.989h-.524v7.968a2.665,2.665,0,0,1-2.663,2.656h-5.715l-1.133,1.055h4.5l3.032,3.039a.531.531,0,0,0,.907-.376V87.669h1.594a1.589,1.589,0,0,0,1.594-1.587v-8.5A1.6,1.6,0,0,0,193.666,75.989Z" transform="translate(-183.631 -75.989)" fill="#fff"/>
                                </g>
                              </g>
                            </g>
                          </svg>
                        </span>
                        <span class="status-icon">
                          <svg xmlns="http://www.w3.org/2000/svg" width="10" height="10" viewBox="0 0 10 10">
                            <circle id="Ellipse_100" data-name="Ellipse 100" cx="5" cy="5" r="5" fill="#FFFFFF"/>
                          </svg>
                        </span>
                    </div>
                  </b-col>
                </b-row>
              </div>
            </div>
          </div>
        </b-modal>

        <!-- Coinflip Match -->
        <b-modal ref="coinflip-match-modal" id="coinflip-match-modal"  hide-footer hide-header>
          <div class="coinflip-match-content">
            <div class="coinflip-match-header">
              <b-row>
                <b-col class="text-center">
                  <h5 class="mb-0">Coinflip Match</h5>
                  <span @click="closeCoinflipModal" class="modal-close">&times;</span>
                </b-col>
              </b-row>
            </div>

            <div class="coinflip-match-body">
              <b-row class="top-row">
                <b-col cols="3" xs="3" md="2">
                  <div class="box-item text-center pt-2 mt-1">
                    <svg id="contentBoxSvgIcon" xmlns="http://www.w3.org/2000/svg" width="25" height="35" viewBox="0 0 13 14.477">
                      <path id="XMLID_88_" d="M126.76,4.279A5.375,5.375,0,0,1,135.076.955l.25.173-.44.987a4.8,4.8,0,0,0-1.981-.409,4.667,4.667,0,0,0-.556.033V1.18h-.733v.707a4.619,4.619,0,0,0-1.263.585l-.488-.633-.581.448.491.637a4.673,4.673,0,0,0-.824,1l-.728-.212-.205.7.6.174a4.614,4.614,0,0,0-.346,1.757v.769h-1.338l-.076-.266a5.385,5.385,0,0,1-.092-2.569Z" transform="translate(-126.647 0)" fill="#FFA30F"/>
                      <path id="XMLID_90_" d="M74.493,103.681A3.91,3.91,0,0,1,78.4,99.775a4.073,4.073,0,0,1,3.718,2.35,5.687,5.687,0,0,1-2.241,1.252A1.353,1.353,0,1,0,78.34,105.6a2.171,2.171,0,0,0-.59,1.153,5.4,5.4,0,0,1-1.337,2.954l-.107.107h-.649a2.487,2.487,0,0,1-1.05-.23,2.521,2.521,0,0,1-.858-.649l-.18-.21.153-.23a3.6,3.6,0,0,0,.77-2.207Z" transform="translate(-72.141 -97.337)" fill="#FFA30F"/>
                      <path id="XMLID_107_" d="M31.062,202.09a1.348,1.348,0,0,0-.071-.433,6.486,6.486,0,0,0,2.646-1.683l.007-.008.086-.094.007.053.023.178c.044.342.072.574.087.786A11.025,11.025,0,0,1,33.8,202.4l-.024.362-.219,0a2.031,2.031,0,0,0-1.3.51,1.642,1.642,0,0,0-.45,1.153l.148,1.7a1.975,1.975,0,0,1-.593.187,3.441,3.441,0,0,1-.737,0l-.87-2.725v-.144A1.356,1.356,0,0,0,31.062,202.09Z" transform="translate(-22.811 -194.987)" fill="#FFA30F"/>
                      <path id="XMLID_109_" d="M174.776,266.447a.621.621,0,1,1,.621-.621A.622.622,0,0,1,174.776,266.447Z" transform="translate(-167.879 -258.723)" fill="#FFA30F"/>
                    </svg>
                  </div>
                </b-col>
                <b-col cols="6" xs="6" md="7" >
                  <h6 class="text-white mb-0 mt-2">Griffin Wooldridge</h6>
                  <small class="color-gray">Total Pot: <span class="color-yellow">4 mbtc</span></small>
                </b-col>
                <b-col cols="3">
                  <div class="box-item box-item-right text-center pt-2 mt-1">
                    <svg id="contentBoxSvgIcon" xmlns="http://www.w3.org/2000/svg" width="25" height="35" viewBox="0 0 13 14.477">
                      <path id="XMLID_88_" d="M126.76,4.279A5.375,5.375,0,0,1,135.076.955l.25.173-.44.987a4.8,4.8,0,0,0-1.981-.409,4.667,4.667,0,0,0-.556.033V1.18h-.733v.707a4.619,4.619,0,0,0-1.263.585l-.488-.633-.581.448.491.637a4.673,4.673,0,0,0-.824,1l-.728-.212-.205.7.6.174a4.614,4.614,0,0,0-.346,1.757v.769h-1.338l-.076-.266a5.385,5.385,0,0,1-.092-2.569Z" transform="translate(-126.647 0)" fill="#FFA30F"/>
                      <path id="XMLID_90_" d="M74.493,103.681A3.91,3.91,0,0,1,78.4,99.775a4.073,4.073,0,0,1,3.718,2.35,5.687,5.687,0,0,1-2.241,1.252A1.353,1.353,0,1,0,78.34,105.6a2.171,2.171,0,0,0-.59,1.153,5.4,5.4,0,0,1-1.337,2.954l-.107.107h-.649a2.487,2.487,0,0,1-1.05-.23,2.521,2.521,0,0,1-.858-.649l-.18-.21.153-.23a3.6,3.6,0,0,0,.77-2.207Z" transform="translate(-72.141 -97.337)" fill="#FFA30F"/>
                      <path id="XMLID_107_" d="M31.062,202.09a1.348,1.348,0,0,0-.071-.433,6.486,6.486,0,0,0,2.646-1.683l.007-.008.086-.094.007.053.023.178c.044.342.072.574.087.786A11.025,11.025,0,0,1,33.8,202.4l-.024.362-.219,0a2.031,2.031,0,0,0-1.3.51,1.642,1.642,0,0,0-.45,1.153l.148,1.7a1.975,1.975,0,0,1-.593.187,3.441,3.441,0,0,1-.737,0l-.87-2.725v-.144A1.356,1.356,0,0,0,31.062,202.09Z" transform="translate(-22.811 -194.987)" fill="#FFA30F"/>
                      <path id="XMLID_109_" d="M174.776,266.447a.621.621,0,1,1,.621-.621A.622.622,0,0,1,174.776,266.447Z" transform="translate(-167.879 -258.723)" fill="#FFA30F"/>
                    </svg>
                  </div>
                </b-col>
              </b-row>

              <b-row class="middle-row mt-4">
                <b-col cols="3" xs="3" md="2">
                  <div class="box-item text-center pt-2 mt-1">
                    <svg id="contentBoxSvgIcon" xmlns="http://www.w3.org/2000/svg" width="25" height="35" viewBox="0 0 13 14.477">
                      <path id="XMLID_88_" d="M126.76,4.279A5.375,5.375,0,0,1,135.076.955l.25.173-.44.987a4.8,4.8,0,0,0-1.981-.409,4.667,4.667,0,0,0-.556.033V1.18h-.733v.707a4.619,4.619,0,0,0-1.263.585l-.488-.633-.581.448.491.637a4.673,4.673,0,0,0-.824,1l-.728-.212-.205.7.6.174a4.614,4.614,0,0,0-.346,1.757v.769h-1.338l-.076-.266a5.385,5.385,0,0,1-.092-2.569Z" transform="translate(-126.647 0)" fill="#5417B1"/>
                      <path id="XMLID_90_" d="M74.493,103.681A3.91,3.91,0,0,1,78.4,99.775a4.073,4.073,0,0,1,3.718,2.35,5.687,5.687,0,0,1-2.241,1.252A1.353,1.353,0,1,0,78.34,105.6a2.171,2.171,0,0,0-.59,1.153,5.4,5.4,0,0,1-1.337,2.954l-.107.107h-.649a2.487,2.487,0,0,1-1.05-.23,2.521,2.521,0,0,1-.858-.649l-.18-.21.153-.23a3.6,3.6,0,0,0,.77-2.207Z" transform="translate(-72.141 -97.337)" fill="#5417B1"/>
                      <path id="XMLID_107_" d="M31.062,202.09a1.348,1.348,0,0,0-.071-.433,6.486,6.486,0,0,0,2.646-1.683l.007-.008.086-.094.007.053.023.178c.044.342.072.574.087.786A11.025,11.025,0,0,1,33.8,202.4l-.024.362-.219,0a2.031,2.031,0,0,0-1.3.51,1.642,1.642,0,0,0-.45,1.153l.148,1.7a1.975,1.975,0,0,1-.593.187,3.441,3.441,0,0,1-.737,0l-.87-2.725v-.144A1.356,1.356,0,0,0,31.062,202.09Z" transform="translate(-22.811 -194.987)" fill="#5417B1"/>
                      <path id="XMLID_109_" d="M174.776,266.447a.621.621,0,1,1,.621-.621A.622.622,0,0,1,174.776,266.447Z" transform="translate(-167.879 -258.723)" fill="#5417B1"/>
                    </svg>
                  </div>
                </b-col>
                <b-col cols="6" xs="6" md="7" class="pt-2" >
                  <h6 class="text-white mb-0 mt-2">Griffin Wooldridge</h6>
                </b-col>

                <b-col cols="3" class="text-end">
                  <svg xmlns="http://www.w3.org/2000/svg" width="35" height="46.957" viewBox="0 0 46.591 46.957">
                    <g id="Group_61" data-name="Group 61" transform="translate(-954.257 -179.133)">
                      <g id="Group_19" data-name="Group 19" transform="translate(954.257 179.133)">
                        <g id="Group_6" data-name="Group 6" transform="translate(0 0)">
                          <g id="swords" transform="translate(0 0)">
                            <path id="Path_14" data-name="Path 14" d="M174.53,38.4h4.433L201.6,15.766l-4.433-4.433L174.53,33.967Z" transform="translate(-174.53 7.889)" fill="#c6c5ca"/>
                            <path id="Path_15" data-name="Path 15" d="M197.164,15.766,174.53,38.4h2.281l22.634-22.634-4.433-4.433-1.14,1.14Z" transform="translate(-172.378 7.889)" fill="#79758a"/>
                            <g id="Group_4" data-name="Group 4" transform="translate(25.178 0)">
                              <rect id="Rectangle_45" data-name="Rectangle 45" width="15.984" height="3.13" transform="translate(2.213 7.896) rotate(45)" fill="#3b0f80"/>
                              <rect id="Rectangle_46" data-name="Rectangle 46" width="7.561" height="2.266" transform="translate(16.067 0) rotate(45)" fill="#461298"/>
                            </g>
                            <g id="Group_5" data-name="Group 5" transform="translate(26.229)">
                              <rect id="Rectangle_47" data-name="Rectangle 47" width="5.179" height="13.113" transform="translate(14.255 2.445) rotate(45)" fill="#5417b1"/>
                              <path id="Path_16" data-name="Path 16" d="M116.616,253.978l-1.051,1.051,1.163,1.163,2.213-2.214-11.3-11.3-1.163,1.163Z" transform="translate(-106.477 -234.779)" fill="#5417b1"/>
                              <path id="Path_17" data-name="Path 17" d="M15.88,422.3l-.807.807.795.795,1.6-1.6-5.346-5.346-.795.795Z" transform="translate(2.893 -416.956)" fill="#5417b1"/>
                            </g>
                            <path id="Path_18" data-name="Path 18" d="M49.255,319.035l-8.478,8.478.795.795,9.273-9.273-3.662-3.662-.795.795Z" transform="translate(-6.698 -312.929)" fill="#3b0f80"/>
                          </g>
                        </g>
                        <g id="Group_7" data-name="Group 7" transform="translate(0 0)">
                          <g id="swords-2" data-name="swords" transform="translate(0)">
                            <path id="Path_14-2" data-name="Path 14" d="M201.6,38.4h-4.433L174.53,15.766l4.433-4.433L201.6,33.967Z" transform="translate(-155.006 7.889)" fill="#c6c5ca"/>
                            <path id="Path_15-2" data-name="Path 15" d="M176.811,15.766,199.445,38.4h-2.281L174.53,15.766l4.433-4.433,1.14,1.14Z" transform="translate(-155.006 7.889)" fill="#79758a"/>
                            <g id="Group_4-2" data-name="Group 4" transform="translate(0 0)">
                              <rect id="Rectangle_45-2" data-name="Rectangle 45" width="15.984" height="3.13" transform="translate(21.413 10.11) rotate(135)" fill="#3b0f80"/>
                              <path id="Path_97" data-name="Path 97" d="M0,0H7.561V2.266H0Z" transform="translate(6.948 1.602) rotate(135)" fill="#45168e"/>
                            </g>
                            <g id="Group_5-2" data-name="Group 5" transform="translate(0)">
                              <rect id="Rectangle_47-2" data-name="Rectangle 47" width="5.179" height="13.113" transform="translate(15.379 11.717) rotate(135)" fill="#5417b1"/>
                              <path id="Path_16-2" data-name="Path 16" d="M108.8,253.978l1.051,1.051-1.163,1.163-2.214-2.214,11.3-11.3,1.163,1.163Z" transform="translate(-98.58 -234.779)" fill="#5417b1"/>
                              <path id="Path_17-2" data-name="Path 17" d="M12.917,422.3l.807.807-.795.795-1.6-1.6,5.346-5.346.795.795Z" transform="translate(-11.328 -416.956)" fill="#5417b1"/>
                            </g>
                            <path id="Path_18-2" data-name="Path 18" d="M42.366,319.035l8.478,8.478-.795.795-9.273-9.273,3.662-3.662.795.795Z" transform="translate(-38.332 -312.929)" fill="#3b0f80"/>
                          </g>
                        </g>
                      </g>
                      <g id="shield" transform="translate(959.006 182.441)">
                        <path id="Path_86" data-name="Path 86" d="M154.621,148.669c.262,4.894.259,25.728-17.671,35.731a1.09,1.09,0,0,1-1.044.008c-18.185-9.771-18.447-30.734-18.24-35.69a1.078,1.078,0,0,1,1.095-1.031,23.829,23.829,0,0,0,16.764-6.5,1.075,1.075,0,0,1,1.5,0,23.6,23.6,0,0,0,16.512,6.455A1.079,1.079,0,0,1,154.621,148.669Z" transform="translate(-117.635 -140.888)" fill="#252233"/>
                        <path id="Path_87" data-name="Path 87" d="M175.253,182.856a36.363,36.363,0,0,1-.133,5.29l-.04,0-4.353,1.621a29.1,29.1,0,0,1-20.287,0l-4.357-1.621h0a36.674,36.674,0,0,1-.189-5.249.856.856,0,0,1,.871-.82,18.931,18.931,0,0,0,13.319-5.16.854.854,0,0,1,1.192,0,18.752,18.752,0,0,0,13.118,5.129A.856.856,0,0,1,175.253,182.856Z" transform="translate(-142.06 -171.849)" fill="#c6c5ca"/>
                        <path id="Path_88" data-name="Path 88" d="M176.44,261.74l.04,0c-.64,6.691-3.4,17.237-13.907,23.1a.866.866,0,0,1-.829.007c-10.7-5.752-13.593-16.384-14.3-23.11h0l4.357,1.621a29.1,29.1,0,0,0,20.287,0Z" transform="translate(-143.422 -245.446)" fill="#b8b7bf"/>
                        <path id="Path_95" data-name="Path 95" d="M150.323,189.721c-.081-.545-.146-1.073-.2-1.577a36.677,36.677,0,0,1-.189-5.249.856.856,0,0,1,.871-.82,18.974,18.974,0,0,0,11.888-3.932,16.5,16.5,0,0,1-1.422-1.225.854.854,0,0,0-1.192,0,18.931,18.931,0,0,1-13.319,5.16.856.856,0,0,0-.871.82,36.675,36.675,0,0,0,.189,5.249h0Z" transform="translate(-142.06 -171.85)" fill="#79758a"/>
                        <path id="Path_96" data-name="Path 96" d="M151.684,263.318l-4.242-1.577h0c.712,6.726,3.6,17.358,14.3,23.11a.866.866,0,0,0,.829-.007q.819-.457,1.575-.951C155.527,278.448,152.618,269.65,151.684,263.318Z" transform="translate(-143.422 -245.447)" fill="#79758a"/>
                      </g>
                    </g>
                  </svg>
                </b-col>
              </b-row>

              <b-row class="mt-4 third-row">
                <b-col cols="12" class="text-center">
                  <span class="text-white">Griffin Wooldridge.</span>
                  <small class="text-gray"> Has won this coinflip <br/> e9ffd2083f6fa712487bda0ebfcc6e3a7fc809a9d02755d214209...</small>
                </b-col>
              </b-row>

              <b-row class="mt-4">
                <b-col>
                  <b-button class="w-100 btn join-button">Join</b-button>
                </b-col>
              </b-row>
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
      //Notification Data
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
      ],

      // Staff Online Data
      onlineUser: true,
      onlineUsers: [
        { 'title': 'Griffin Wooldridge', status: 1},
        { 'title': 'Griffin Wooldridge', status: 2},
        { 'title': 'Griffin Wooldridge', status: 3},
        { 'title': 'Griffin Wooldridge', status: 4}
      ],
      offlineUsers: [
        { 'title': 'Griffin Wooldridge', status: 1},
        { 'title': 'Griffin Wooldridge', status: 2},
        { 'title': 'Griffin Wooldridge', status: 3},
        { 'title': 'Griffin Wooldridge', status: 4},
        { 'title': 'Griffin Wooldridge', status: 1},
        { 'title': 'Griffin Wooldridge', status: 2},
        { 'title': 'Griffin Wooldridge', status: 3},
        { 'title': 'Griffin Wooldridge', status: 4}
      ],

      //Coinflip Data
    }
  },
  methods: {
    //Notification Modal Method
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
    },

    // Staff Online Method
    staffOnlineColorBindingClass(status) {
      switch(status) {
        case 1:
          return 'color-yellow';
        case 2:
          return 'color-white';
        case 3:
          return 'color-gray';
        case 4:
          return 'color-red';    
        default:
          return 'color-white';  
      }
    },

    closeStaffModal() {
      this.$refs['staff-online-modal'].hide();
    },

    //Confilp Match Modal Method
    closeCoinflipModal() {
      this.$refs['coinflip-match-modal'].hide();
    }
  }
}
</script>

<style lang="scss">
  // Notification Modal CSS
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

  // Staff-online Modal CSS
  #staff-online-modal {
    .modal-content {
      background-color: #252233;
      border-radius: 20px;
      .modal-body {
        padding: 0px !important;
        .staff-online-content {
          .staff-online-header {
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

          .staff-online-body {
            padding: 30px;
            .cursor-pointer {
              cursor: pointer;
            }
            .content-title {
              color: #FFFFFF;
            }
            .content-box {
              padding: 15px;
              background-color: #1D1A2A;
              border-radius: 10px;
              color: #FFA30F;
              .content-box-svg-icon {
                path {
                  fill: #FFA30F;
                }
              }

              .title {
                font-size: 13px;
              }

              .message-icon {
                position: absolute;
                right: 50px;
                top: 15px;
                color: #FFFFFF;
              }

              .status-icon {
                position: absolute;
                right: 15px;
                top: 15px;
                color: #FFFFFF;
              }
            }

            .color-white {
              .content-box-svg-icon {
                path {
                  fill: #FFFFFF;
                }
              }
              .title {
                color: #FFFFFF;
              }
            }

            .color-yellow {
              .content-box-svg-icon {
                path {
                  fill: #FFA30F;
                }
              }
              .title {
                color: #FFA30F;
              }
            }

            .color-red {
              .content-box-svg-icon {
                path {
                  fill: #FF1C61;
                }
              }
              .title {
                color: #FF1C61;
              }
            }

            .color-gray {
              .content-box-svg-icon {
                path {
                  fill: #79758A;
                }
              }
              .title {
                color: #79758A;
              }
            }
          }
        }
      }
    }
  }

  // Coinflip Match Modal CSS
  #coinflip-match-modal {
    .modal-content {
      background-color: #252233;
      border-radius: 20px;
      .modal-body {
        padding: 0px !important;
        .coinflip-match-content {
          .coinflip-match-header {
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

          .coinflip-match-body {
            padding: 30px 45px;
            .top-row {
              background-color: #171424;
              border-radius: 40px;
              border: 2px solid #FFA30F;
              padding: 10px;
              .box-item {
                width: 50px;
                height: 50px;
                border-radius: 50%;
                border: 2px solid #FFA30F;
              }

              .box-item-right {
                float: right;
              }

              .color-gray {
                color: #79758A;
              }

              .color-yellow {
                color: #FFA30F;
              }
            }

            .middle-row {
              .box-item {
                width: 50px;
                height: 50px;
                border-radius: 50%;
                border: 2px solid #5417B1;
              }

              .box-item-right {
                float: right;
              }
            }

            .third-row {
              .col-12 {
                line-height: 0.9rem;
                .text-gray {
                  color: #79758A;
                  font-size: 10px;
                }
              }
            }

            .join-button {
              background-color: #5417B1;
              color: #FFFFFF;
              border: 0px;
              border-radius: 10px;
              padding: 10px;
            }
          }
        }
      }
    }
  }
</style>

