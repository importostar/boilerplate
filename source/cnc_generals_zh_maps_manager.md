---
title: cnc_generals_zh_maps_manager
date: 2020-05-07
---
Example Python program cnc_generals_zh_maps_manager.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtWidgets import QApplication, QMainWindow, QDesktopWidget, QTableWidget, QTableWidgetItem, QHeaderView, QAbstractItemView
* from PyQt5.QtCore import Qt
* from PyQt5.QtGui import QPixmap
* from urllib.parse import unquote
* from PIL import Image, ImageDraw
* import logging
* import os
* import re
* import sys

## Classes

* class Map:
* class MapCacheParser:
* class CnCGeneralsAndZeroHourMapsManager(QMainWindow):

## Methods

* def __init__(self):
* def build_minimap(self):
* def _draw_circle(self, surface, pos, diameter=6, fill=None, outline=None):
* def __repr__(self):
* def __init__(self, path):
* def parse(self):
* def search(self, num_players=None):
* def build_minimaps(self):
* def _process_param(self, param):
* def _parse_coords(self, coords):
* def _snake_case(self, name):
* def __init__(self):
* def createMapsTable(self):
* def center(self):

## Code

Example Python PyQt program :

    from PyQt5.QtWidgets import QApplication, QMainWindow, QDesktopWidget, QTableWidget, QTableWidgetItem, QHeaderView, QAbstractItemView
    from PyQt5.QtCore import Qt
    from PyQt5.QtGui import QPixmap
    from urllib.parse import unquote
    from PIL import Image, ImageDraw
    import logging
    import os
    import re
    import sys
    
    
    class Map:
        def __init__(self):
            self.techs_position = []
            self.supplies_position = []
            self.players_position = []
    
        def build_minimap(self):
            tga_minimap_path = self.file_path.replace('.map', '.tga')
            png_minimap_path = self.file_path.replace('.map', '.png')
    
            if not os.path.isfile(tga_minimap_path):
                raise FileNotFoundError('The TGA minimap image was not found: {}'.format(tga_minimap_path))
    
            tga_minimap = Image.open(tga_minimap_path)
    
            tga_minimap_draw = ImageDraw.Draw(tga_minimap)
    
            for tech_position in self.techs_position:
                x_pos_on_minimap = (tech_position[0] * tga_minimap.width) / self.map_size[0]
                y_pos_on_minimap = (tech_position[1] * tga_minimap.height) / self.map_size[1]
    
                self._draw_circle(tga_minimap_draw, (x_pos_on_minimap, y_pos_on_minimap), diameter=4, fill='yellow', outline='black')
    
            for supply_position in self.supplies_position:
                x_pos_on_minimap = (supply_position[0] * tga_minimap.width) / self.map_size[0]
                y_pos_on_minimap = (supply_position[1] * tga_minimap.height) / self.map_size[1]
    
                self._draw_circle(tga_minimap_draw, (x_pos_on_minimap, y_pos_on_minimap), diameter=4, fill='green', outline='black')
    
            for player_position in self.players_position:
                x_pos_on_minimap = (player_position[0] * tga_minimap.width) / self.map_size[0]
                y_pos_on_minimap = (player_position[1] * tga_minimap.height) / self.map_size[1]
    
                self._draw_circle(tga_minimap_draw, (x_pos_on_minimap, y_pos_on_minimap), diameter=8, fill='lightblue', outline='black')
    
            tga_minimap.save(png_minimap_path, 'PNG')
    
        def _draw_circle(self, surface, pos, diameter=6, fill=None, outline=None):
            radius = abs(diameter / 2)
    
            elipse_pos = [
                pos[0] - radius,
                pos[1] - radius,
                pos[0] + radius,
                pos[1] + radius
            ]
    
            surface.ellipse(elipse_pos, fill=fill, outline=outline)
    
        def __repr__(self):
            return str(self.__dict__)
    
    
    class MapCacheParser:
        _maps = []
    
        def __init__(self, path):
            self._path = path
    
            if not os.path.isfile(self._path):
                raise FileNotFoundError('The MapCache file was not found: {}'.format(self._path))
    
        def parse(self):
            with open(self._path, 'r') as f:
                current_map = None
                in_map_section = False
    
                for line in f:
                    line = line.strip()
    
                    if not line or line.startswith(';'): # Empty or comment line
                        continue
    
                    if line.startswith('MapCache'): # MapCache section start
                        file_path = unquote(line.replace('MapCache ', '').replace('_', '%'))
    
                        current_map = Map()
                        current_map.file_path = file_path
                        current_map.name = os.path.splitext(os.path.basename(file_path))[0].title()
    
                        in_map_section = True
                    elif line == 'END': # MapCache section end
                        self._maps.append(current_map)
    
                        current_map = None
                        in_map_section = False
                    elif in_map_section: # MapCache section key and values
                        param = [s.strip() for s in line.split('=', maxsplit=1)]
    
                        if len(param) != 2:
                            continue
    
                        name, value = self._process_param(param)
    
                        if value is None:
                            continue
    
                        if name == 'techPosition':
                            current_map.techs_position.append(value)
                        elif name == 'supplyPosition':
                            current_map.supplies_position.append(value)
                        elif name.startswith('Player_') and name.endswith('_Start'):
                            current_map.players_position.append(value)
                        else:
                            setattr(current_map, name, value)
    
        def search(self, num_players=None):
            results = []
    
            for map in self._maps:
                num_players_match = False
    
                if num_players is not None:
                    num_players_match = map.num_players == num_players
    
                if num_players_match:
                    results.append(map)
    
            return results
    
        def build_minimaps(self):
            for map in self._maps:
                try:
                    map.build_minimap()
                except Exception as e:
                    logging.error(e)
    
        def _process_param(self, param):
            name, value = param
    
            # Value processing
            if name in ['numPlayers', 'fileSize']:
                value = int(value)
            elif name in ['isOfficial', 'isMultiplayer']:
                value = value == 'yes'
            elif name in ['extentMax', 'techPosition', 'supplyPosition'] or (name.startswith('Player_') and name.endswith('_Start')):
                value = self._parse_coords(value)
            else:
                value = None # Invalid values will be removed
    
            # Name processing
            if name in ['numPlayers', 'fileSize', 'isOfficial', 'isMultiplayer']:
                name = self._snake_case(name)
            elif name == 'extentMax':
                name = 'map_size'
    
            return name, value
    
        def _parse_coords(self, coords):
            x, y, z = coords.replace('X:', '').replace('Y:', '').replace('Z:', '').split(' ')
    
            return (float(x), float(y), float(z))
    
        def _snake_case(self, name):
            s1 = re.sub('(.)([A-Z][a-z]+)', r'\1_\2', name)
    
            return re.sub('([a-z0-9])([A-Z])', r'\1_\2', s1).lower()
    
    
    class CnCGeneralsAndZeroHourMapsManager(QMainWindow):
        def __init__(self):
            super().__init__()
    
            self.resize(800, 600)
    
            self.setWindowTitle('C&C Generals & Zero Hour Maps Manager')
    
            self.createMapsTable()
    
            self.center()
            self.show()
    
        def createMapsTable(self):
            mcp = MapCacheParser('C:\\Users\\Maxime GROSS\\Documents\\Command and Conquer Generals Zero Hour Data\\Maps\\MapCache.ini')
    
            mcp.parse()
            #mcp.build_minimaps()
    
            self.maps_table = QTableWidget(len(mcp._maps), 7)
            self.maps_table.setFocusPolicy(Qt.NoFocus)
            self.maps_table.setSelectionBehavior(QTableWidget.SelectRows)
            self.maps_table.setEditTriggers(QAbstractItemView.NoEditTriggers)
            self.maps_table.setHorizontalHeaderLabels([
                'Preview',
                'Name',
                'Official?',
                'Multiplayer?',
                'Players',
                'Capturable buildings',
                'Supply points'
            ])
    
            maps_table_vertical_header = self.maps_table.verticalHeader()
            maps_table_vertical_header.hide()
    
            maps_table_horizontal_header = self.maps_table.horizontalHeader()
            maps_table_horizontal_header.setSectionResizeMode(QHeaderView.ResizeToContents)
            maps_table_horizontal_header.setStretchLastSection(True)
    
            i = 0
    
            for map in mcp._maps:
                png_minimap_path = map.file_path.replace('.map', '.png')
    
                if os.path.isfile(png_minimap_path):
                    minimap_pixmap = QPixmap(png_minimap_path)
    
                    minimap_cell = QTableWidgetItem()
                    minimap_cell.setData(Qt.DecorationRole, minimap_pixmap)
    
                    self.maps_table.setItem(i, 0, minimap_cell)
                else:
                    self.maps_table.setItem(i, 0, QTableWidgetItem(''))
    
                self.maps_table.setItem(i, 1, QTableWidgetItem(map.name))
                self.maps_table.setItem(i, 2, QTableWidgetItem('Oui' if map.is_official else 'Non'))
                self.maps_table.setItem(i, 3, QTableWidgetItem('Oui' if map.is_multiplayer else 'Non'))
                self.maps_table.setItem(i, 4, QTableWidgetItem(str(map.num_players)))
                self.maps_table.setItem(i, 5, QTableWidgetItem(str(len(map.techs_position))))
                self.maps_table.setItem(i, 6, QTableWidgetItem(str(len(map.supplies_position))))
    
                i += 1
    
            self.maps_table.setSortingEnabled(True)
            self.maps_table.resizeRowsToContents()
            self.setCentralWidget(self.maps_table)
    
        def center(self):
            qr = self.frameGeometry()
            cp = QDesktopWidget().availableGeometry().center()
            qr.moveCenter(cp)
            self.move(qr.topLeft())
    
    if __name__ == '__main__':
        logging.basicConfig(
            format='%(asctime)s - %(levelname)s - %(message)s',
            datefmt='%d/%m/%Y %H:%M:%S',
            stream=sys.stdout
        )
    
        logging.getLogger().setLevel(logging.INFO)
    
        app = QApplication(sys.argv)
        cnc_generals_zh_maps_manager = CnCGeneralsAndZeroHourMapsManager()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
