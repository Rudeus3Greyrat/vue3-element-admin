<script>
const ItemRendering = (props, context) => {
  const { icon, title } = props
  const vnodes = []

  if (icon) {
    if (icon.includes('el-icon')) {
      vnodes.push(<i class={[icon, 'sub-el-icon']} />)
    } else {
      vnodes.push(<svg-icon icon-class={icon}/>)
    }
  }

  if (title) {
    vnodes.push(<span slot='title'>{(title)}</span>)
  }
  return vnodes
}
ItemRendering.props = {
  icon: {
    type: String,
    default: ''
  },
  title: {
    type: String,
    default: ''
  }
}
export default ItemRendering
</script>

<style scoped>
.sub-el-icon {
  color: currentColor;
  width: 1em;
  height: 1em;
}
</style>
