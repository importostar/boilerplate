---
title: UserView3
date: 2020-05-07
---
Example Python program UserView3.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from flask import request, json, Response, Blueprint, g
* from ..models.UserModel import UserModel, UserSchema
* from ..shared.Authentication import Auth

## Methods

* def get_a_user(user_id):
* def update():
* def delete():
* def get_me():

## Code

Python example

    #/src/views/UserView
    
    from flask import request, json, Response, Blueprint, g
    from ..models.UserModel import UserModel, UserSchema
    from ..shared.Authentication import Auth
    
    user_api = Blueprint('user_api', __name__)
    user_schema = UserSchema()
    
    
    #####################
    # existing code remains #
    ########################
    
    @user_api.route('/<int:user_id>', methods=['GET'])
    @Auth.auth_required
    def get_a_user(user_id):
      """
      Get a single user
      """
      user = UserModel.get_one_user(user_id)
      if not user:
        return custom_response({'error': 'user not found'}, 404)
      
      ser_user = user_schema.dump(user).data
      return custom_response(ser_user, 200)
    
    @user_api.route('/me', methods=['PUT'])
    @Auth.auth_required
    def update():
      """
      Update me
      """
      req_data = request.get_json()
      data, error = user_schema.load(req_data, partial=True)
      if error:
        return custom_response(error, 400)
    
      user = UserModel.get_one_user(g.user.get('id'))
      user.update(data)
      ser_user = user_schema.dump(user).data
      return custom_response(ser_user, 200)
    
    @user_api.route('/me', methods=['DELETE'])
    @Auth.auth_required
    def delete():
      """
      Delete a user
      """
      user = UserModel.get_one_user(g.user.get('id'))
      user.delete()
      return custom_response({'message': 'deleted'}, 204)
    
    @user_api.route('/me', methods=['GET'])
    @Auth.auth_required
    def get_me():
      """
      Get me
      """
      user = UserModel.get_one_user(g.user.get('id'))
      ser_user = user_schema.dump(user).data
      return custom_response(ser_user, 200)
    
    
    
    #####################
    # existing code remains #
    ########################
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
