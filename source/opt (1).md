---
title: opt (1)
date: 2020-05-07
---
Example Python program opt (1).py

## Modules

* import argparse

## Classes

* class OptParser():

## Methods

* def __init__(self):
* def parse(self):
* def parse_args(self, args):

## Code

Python example

    import argparse
    
    class OptParser():
        def __init__(self):
            parser = argparse.ArgumentParser()
            # Basic information
            parser.add_argument('--name', type=str, default='Face-X', help='Project name')
            parser.add_argument('--tag', type=str, default='0.1', help='Project tag')
            # Params
            # parser.add_argument('--method', required=True, type=str, choices=['shufflenet', 'hourglass'], help='Choose which model method to use')
            parser.add_argument('--mode', required=True, help='train, test')
            parser.add_argument('--gpu', default=False, action='store_true', help='use gpu')
            parser.add_argument('--img_size', type=list, default=[256, 256], help='img size')
            # Dataset
            parser.add_argument('--dataset_root_path', required=True, type=str, default=None, help='')
            parser.add_argument('--dataset_name', required=True, type=str, help='')
            parser.add_argument('--have_dev', default=False, action='store_true', help='Use devset or not')
            parser.add_argument('--dev_ratio', type=float, default=0.1, help='Split dev set from train set when --do_dev=True and --dev_dataset_root=None')
            # Training
            parser.add_argument('--batch_size', type=int, default=1, help='')
            parser.add_argument('--num_epoch', type=int, default=1, help='num epoch')
            parser.add_argument('--shuffle', default=False, action='store_true', help='')
            parser.add_argument('--lr', type=float, default=1e-1, help='')
            parser.add_argument('--weight_decay', type=float, default=1e-3, help='')
            # Save
            parser.add_argument('--checkpoint_save_path', required=True, help='where to save checkpoint')
            parser.add_argument('--save_latest_ckp_num_per_epoch', type=int, default=2, help='save model at iter')
            # parser.add_argument('--save_latest_epoch_freq', type=int, requdefault=0, help='save model at epoch')
            # Loss
            # TODO:
            # test other loss
            ## wing loss
            parser.add_argument('--wing_loss_weight', type=float, default=10, help='')
            parser.add_argument('--wing_loss_epsilon', type=float, default=2, help='')
            # Model
            ## mobilenetv2
            parser.add_argument('--mobilenetv2_num_out', type=int, default=18)
            parser.add_argument('--mobilenetv2_input_size', type=int, default=224)
            parser.add_argument('--mobilenetv2_width_mult', type=int, default=1.0)
            ## TODO: Add other model: Resnet, shufflenetv2
    
            # Warm start
            parser.add_argument('--warm_start', default=False, action='store_true', help='load ckp to warm start')
            parser.add_argument('--ckp_path', default=None, type=str, help='warm-start checkpoint path')
    
            # Visual
            parser.add_argument('--visual', action='store_true', help='Using visdom visual loss and result')
            parser.add_argument('--visdom_server_ip', type=str, default='http://127.0.0.1', help='')
            parser.add_argument('--visdom_port', type=int, default=8097, help='')
            parser.add_argument('--visdom_env', type=str, default='main', help='')
            parser.add_argument('--visual_freq', type=int, default=1, help='')
    
            self.__parser = parser
        
        def parse(self):
            return self.__parser.parse_args()
    
        def parse_args(self, args):
            return self.__parser.parse_args(args)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
